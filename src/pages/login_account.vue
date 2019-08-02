<template>
  <div>
    <Header>
      <NavBar @click-left="onClickLeft">
        <button class="back-btn" slot="left"></button>
      </NavBar>
    </Header>
    <div class="login-container">
      <div class="u-tt">欢迎登录易挖</div>
      <div class="login-form">
        <div class="u-label">
          <div class="label">账户</div>
        </div>

        <div class="input-wrap">
          <Field
            placeholder="请输入账户,限手机号"
            v-model.trim="data.mobile"
            @input="setMobile"
            maxlength="11"
            :border="false"
          />
          <!-- <input
            type="text"
            id="account"
            placeholder="请输入账户,限手机号"
            maxlength="11"
            oninput="changeBtnColor()"
          />-->
          <div class="error" v-if="!$v.data.mobile.phone">手机号格式不正确</div>
        </div>
        <div class="u-label">
          <div class="label">密码</div>
        </div>
        <div class="input-wrap">
          <Field
            v-model="data.password"
            type="password"
            placeholder="请输入登录密码"
            @input="$v.data.password.$touch()"
            maxlength="18"
          />
          <div class="error" v-if="!$v.data.password.minLength">密码不能小于6位</div>

          <!-- <input
            type="password"
            id="password"
            maxlength="18"
            placeholder="请输入登录密码"
            oninput="changeBtnColor()"
          />-->
        </div>
        <div class="u-forget" @click="fnOpenWin('forget_password')">忘记密码？</div>
        <div
          class="u-btn"
          id="handle-login"
          :class="allowSubmit?'allow':''"
          @click="handleLogin()"
        >登录</div>
      </div>
      <div class="u-register">
        没有账号？
        <span @click="fnOpenWin('register')">去注册</span>
      </div>
    </div>
  </div>
</template>

<script>
import Header from "@/components/header.vue";

import Vuelidate from "vuelidate";
Vue.use(Vuelidate);
import {
  required,
  minLength,
  maxLength,
  between
} from "vuelidate/lib/validators";
import { phone } from "@/libs/validate.js";

import { NavBar, Field, Toast } from "vant";

import axios from "axios";
window.login_accountVue = {
  name: "login_account",
  components: { Header, NavBar, Field },
  data() {
    return {
      data: {
        mobile: "",
        password: ""
      },
      view: {}
    };
  },
  validations: {
    data: {
      mobile: {
        required,
        phone
      },
      password: {
        required,
        minLength: minLength(6)
      }
    }
  },
  computed: {
    allowSubmit() {
      return !this.$v.data.mobile.$invalid && !this.$v.data.password.$invalid
        ? true
        : false;
    }
  },
  mounted() {
    this.view = JSON.parse(window.localStorage.getItem("view"));
  },
  methods: {
    setMobile(value) {
      // alert(value);
      // this.mobile = value;
      // this.$v.mobile.$touch();
      // console.log(this.$v.data.mobile.$invalid)
      // console.log(this.$v.data.password.$invalid)

      console.log(this.allowSubmit);
    },

    fnOpenWin(name) {
      this.$ac.openWin({
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
    },
    onClickLeft() {
      this.$ac.closeWin();
    },
    handleLogin() {
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
          .post(`http://clientapi.61lu.com/user/login`, formData)
          .then(res => {
            Toast.clear();

            if (res.data.code === 1) {
              window.localStorage.setItem(
                "account",
                JSON.stringify({
                  mobile: res.data.user.mobile,
                  token: res.data.user.token,
                  uid: res.data.user.uid
                })
              );
              Toast.success({
                message: "登录成功",
                onClose() {
                  that.$ac.sendEvent({
                    name: "login",
                    extra: {
                      msg: "登录成功"
                    }
                  });
                  that.$ac.closeWin();
                }
              });
            } else {
              Toast.fail(res.data.desc);
            }
          });
      }
    },
    fnOpenFrame(name) {
      this.$ac.openFrame({
        name: name,
        url: `${name}.html`,
        rect: {
          x: 0,
          y: this.view.headerHeight,
          w: "auto",
          h: this.view.frameHeight
        },
        reload: true,
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

export default window.login_accountVue;
</script>

<style lang="scss" scoped>
@import "@/css/common.scss";
* {
  touch-action: pan-y;
}
.error {
  position: absolute;
  /* right: 0; */
  top: 0;
  right: 0;
  /* transform: translateY(-50%); */
  top: 12px;
  color: red;
}
.back-btn {
  background: url(../images/iconclose.png) no-repeat left center;
  background-size: 12px 12px;
  padding: 22px;
}
.login-container {
  padding: 0 18px;
  box-sizing: border-box;
}

.login-container .u-tt {
  font-size: 19px;
  color: #161616;
  margin: 12px 0 42px 0;
  /* font-weight: 70; */
}

.login-form .u-label {
  display: flex;
  justify-content: space-between;
  font-size: 13px;
  color: #161616;
}

.login-form .u-label .code {
  font-size: 14px;
  color: #23242a;
}

.login-form .input-wrap {
  display: flex;
  width: 100%;
  justify-content: space-between;
  height: 34px;
  font-size: 12px;
  padding-bottom: 6px;
  padding-top: 12px;
  margin-bottom: 15px;
  position: relative;
}

.login-form .input-wrap::after {
  content: "";
  width: 100%;
  height: 1px;
  background: #efefef;
  position: absolute;
  left: 0;
  bottom: 0;
  transform: scaleY(0.5);
}

.login-form .input-wrap input {
  height: 100%;
  outline: none;
}

.login-form .input-wrap button {
  width: 80px;
  height: 34px;
  background: rgba(246, 129, 33, 1);
  border-radius: 3px;
  font-size: 12px;
  line-height: 34px;
  text-align: center;
  color: #fff;
  outline: none;
  border: none;
}

.login-form .u-btn {
  font-size: 14px;
  color: #fff;
  text-align: center;
  line-height: 42px;
  width: 100%;
  height: 42px;
  background: rgba(255, 214, 179, 1);
  border-radius: 4px;
  margin: 25px 0;
  margin-top: 10px;
  &.allow {
    background: rgba(246, 129, 33, 1);
  }
}

.u-register {
  font-size: 12px;
  color: #999;
  text-align: center;
}

.u-register span {
  color: #f68d38;
}

.u-forget {
  color: #161616;
  font-size: 12px;
  text-align: right;
  width: 20%;
  margin-left: 80%;
  padding-bottom: 10px;
}

#account,
#password {
  width: 100%;
}
</style>