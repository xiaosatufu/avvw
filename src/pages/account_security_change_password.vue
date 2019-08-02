<template>
  <div>
    <Header>
      <NavBar title="修改密码" @click-left="onClickLeft">
        <div class="back-btn" slot="left"></div>
      </NavBar>
    </Header>
    <div class="main">
      <div class="old-password input-warp">
        <p>原密码</p>

        <Field
          class="input"
          v-model="data.old_password"
          type="password"
          placeholder="请输入原密码，限数字、字母"
          @input="$v.data.old_password.$touch()"
          maxlength="18"
          :border="false"
        />
        <div class="error" v-if="!$v.data.old_password.minLength">密码不能小于6位</div>
      </div>
      <div class="new-password input-warp">
        <p>新密码</p>
        <Field
          class="input"
          v-model="data.password"
          type="password"
          placeholder="请输入新密码，限数字、字母"
          @input="$v.data.password.$touch()"
          maxlength="18"
          :border="false"
        />
        <div class="error" v-if="!$v.data.password.minLength">密码不能小于6位</div>
      </div>
      <div class="repeat-new-password input-warp">
        <p>重复密码</p>

        <Field
          class="input"
          v-model="data.repeat_password"
          type="password"
          placeholder="请输入重复密码"
          @input="$v.data.repeat_password.$touch()"
          maxlength="18"
          :border="false"
        />
        <div class="error" v-if="!$v.data.repeat_password.sameAsPassword">密码输入不一致，请重新输入</div>
      </div>
      <div class="btn-submit">
        <button @click="handleResetPwd" :class="allowSubmit?'allow':''">提交</button>
      </div>
    </div>
  </div>
</template>

<script>
import Header from "@/components/header.vue";
import { NavBar, Field, Toast } from "vant";

import axios from "axios";

import Vuelidate from "vuelidate";
Vue.use(Vuelidate);
import { required, minLength, sameAs } from "vuelidate/lib/validators";
window.account_security_change_passwordVue = {
  name: "account_security_change_password",
  components: { Header, NavBar, Field, Toast },
  data() {
    return {
      account: {},
      data: {
        token: "",
        uid: "",
        old_password: "",
        password: "",
        repeat_password: ""
      }
    };
  },

  validations: {
    data: {
      old_password: {
        required,
        minLength: minLength(6)
      },
      password: {
        required,
        minLength: minLength(6)
      },
      repeat_password: {
        sameAsPassword: sameAs("password")
      }
    }
  },
  computed: {
    allowSubmit() {
      return !this.$v.data.old_password.$invalid &&
        !this.$v.data.password.$invalid &&
        !this.$v.data.repeat_password.$invalid
        ? true
        : false;
    }
  },
  mounted() {
    this.$ac.addEventListener(
      {
        name: "viewdisappear"
      },
      function(ret, err) {
        alert("window消失");
        api.closeWin({
          name: api.winName
        });
      }
    );
    this.account = JSON.parse(window.localStorage.getItem("account"));
    this.data.token = this.account.token;
    this.data.uid = this.account.uid;
  },
  methods: {
    onClickLeft() {
      this.$ac.closeWin();
    },
    handleResetPwd() {
      const that = this;
      if (this.allowSubmit) {
        const formData = new FormData();
        Object.keys(this.data).forEach(key => {
          formData.append(key, this.data[key]);
        });
        Toast.loading({
          mask: true,
          message: "加载中..."
        });
        axios
          .post(`http://clientapi.61lu.com/user/resetpwd`, formData)
          .then(res => {
            Toast.clear();

            if (res.data.code === 1) {
              // window.localStorage.setItem(
              //   "account",
              //   JSON.stringify({
              //     mobile: res.data.user.mobile,
              //     token: res.data.user.token,
              //     uid: res.data.user.uid
              //   })
              // );

              window.localStorage.removeItem("account");

              Toast.success({
                message: "修改密码成功，请重新登录",
                onClose() {
                  that.$ac.sendEvent({
                    name: "changePwd",
                    extra: {
                      msg: "修改密码成功"
                    }
                  });
                  window.localStorage.removeItem('account')
                  // that.$ac.closeWin();
                  that.$ac.closeToWin({
                    name:'account_security'
                  })
                  that.$ac.fnOpenWin("login_account");
                }
              });
            } else {
              Toast.fail({
                message: res.data.desc,
                onClose() {
                  that.$ac.fnOpenWin("login_account");
                }
              });
            }
          });
      }
    },

    fnOpenWin(name) {
      api.openWin({
        name: name,
        url: `${name}.html`,
        bgColor: "#fff",
        progress: {
          type: "default", //加载进度效果类型，默认值为 default，取值范围为 default|page，为 page 时，进度效果为仿浏览器类型，固定在页面的顶部
          title: "2229999", //type 为 default 时显示的加载框标题，字符串类型
          text: "8888", //type 为 default 时显示的加载框内容，字符串类型
          color: "red", //type 为 page 时进度条的颜色，默认值为 #45C01A，支持#FFF，#FFFFFF，rgb(255,255,255)，rgba(255,255,255,1.0)等格式
          height: 10 //type 为 page 时进度条高度，默认值为3，数字类型
        }
      });
    }
  }
};

export default window.account_security_change_passwordVue;
</script>

<style lang="scss" scoped>
@import "@/css/common.scss";

.error {
  position: absolute;
  bottom: 21px;
  right: 0;
  color: red;
  font-size: 12px;
}
.input {
  padding: 18px 0;
}
.back-btn {
  background: url(../images/icon_back.png) no-repeat left center;
  background-size: 9px 15px;
  padding: 22px;
}
.main {
  display: flex;
  flex-direction: column;
  margin: 0 14px 0 13px;
}

.main p {
  font-size: 13px;
  font-weight: 400px;
  opacity: 100%;
  color: #161616;
}

.main .input-warp {
  position: relative;
}

.main .input-warp:after {
  content: "";
  width: 100%;
  height: 1px;
  background: #cccccc;
  position: absolute;
  left: 0;
  bottom: 0;
  transform: scaleY(0.5);
}

.main input {
  width: 100%;
  height: 49px;
  border-radius: 0px;
  outline-color: invert;
  outline-style: none;
  outline-width: 0px;
  border: none;
  border-style: none;
  text-shadow: none;
  -webkit-appearance: none;
  -webkit-user-select: text;
  outline-color: transparent;
  box-shadow: none;
  /* border-bottom: 0.5px solid #CCCCCC; */
  margin-top: 5px;
}

.main input::-webkit-input-placeholder {
  width: 157px;
  font-size: 12px;
  font-weight: 400;
  color: rgba(204, 204, 204, 1);
}

.old-password p {
  margin: 25px 0 0 0;
}

.new-password p {
  margin: 15px 0 0 0;
}

.repeat-new-password p {
  margin: 15px 0 0 0;
}

.btn-submit button {
  width: 100%;
  box-sizing: border-box;
  display: block;
  height: 42px;
  background: rgba(255, 214, 179, 1);
  border-radius: 4px;
  /* margin: 36px 14px 0 14px; */
  margin-top: 36px;
  color: #fefefe;
  font-size: 14px;
  text-align: center;
  line-height: 42px;
  opacity: 100%;
  outline: none;
  &.allow {
    background: rgba(246, 129, 33, 1);
  }
}
</style>