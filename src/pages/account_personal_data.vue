<template>
  <div class="personal-wrap">
    <Header>
      <NavBar title="个人资料" @click-left="onClickLeft">
        <div class="back-btn" slot="left"></div>
      </NavBar>
    </Header>
    <div class="main">
      <div class="main-head">
        <div class="head_sculpture">头像</div>
        <div class="icon_head">
          <img src="@/images/icon_avatar.png" alt srcset />
        </div>
      </div>
      <div class="main-phone">
        <div class="telephone-number">手机号</div>
        <div class="phone-number" id="mobile">134****6430</div>
      </div>
    </div>
    <button class="btn-logout" @click="hanldeLogout">退出登录</button>
  </div>
</template>

<script>
import Header from "@/components/header.vue";
import { NavBar } from "vant";
window.account_personal_dataVue = {
  name: "account_personal_data",
  components: { Header, NavBar },
  data() {
    return {
      view: {},
      account: {}
    };
  },
  mounted() {
    // this.$ac.addEventListener(
    //   {
    //     name: "viewdisappear"
    //   },
    //   function(ret, err) {
    //     alert("window消失");
    //     api.closeWin({
    //       name: api.winName
    //     });
    //   }
    // );
    // window.location.reload()
    this.view = JSON.parse(window.localStorage.getItem("view"));
    this.account = JSON.parse(window.localStorage.getItem("account"));
    // alert(JSON.stringify(this.view))
  },
  methods: {
    hanldeLogout() {
      window.localStorage.removeItem("account");
      this.$ac.sendEvent({
        name: "loginout",
        extra: {
          msg: "登出成功"
        }
      });
      this.$ac.closeWin();
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
    },
    onClickLeft() {
      this.$ac.closeWin();
    }
  }
};

export default window.account_personal_dataVue;
</script>

<style lang="scss" scoped>
@import "@/css/common.scss";
.personal-wrap {
  // height: 100%;
  // background: #f8f8f8;
}
.back-btn {
  background: url(../images/icon_back.png) no-repeat left center;
  background-size: 9px 15px;
  padding: 22px;
}
.main-head {
  height: 81px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  position: relative;
  background: #fff;
}

.main-head::after {
  content: "";
  width: 100%;
  height: 1px;
  transform: scaleY(0.5);
  position: absolute;
  background: #efefef;
  right: 0;
  bottom: 0;
  margin-right: -16px;
}

.head_sculpture {
  font-size: 13px;
  line-height: 81px;
  margin-left: 14px;
}

.icon_head img {
  width: 46px;
  height: 46px;
  margin: 17px 15px 18px 0;
}

.main-phone {
  height: 49px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  background: #fff;
}

.telephone-number {
  font-size: 13px;
  line-height: 49px;
  margin-left: 14px;
}

.phone-number {
  font-size: 13px;
  color: #999999;
  line-height: 49px;
  margin-right: 19px;
}

.btn-logout {
  width: 100%;
  height: 49px;
  color: #ed565b;
  font-size: 14px;
  line-height: 49px;
  background: #fff;
  margin-top: 36px;
}
</style>