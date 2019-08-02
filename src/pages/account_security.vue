<template>
  <div>
    <Header>
      <NavBar title="账户安全" @click-left="onClickLeft">
        <div class="back-btn" slot="left"></div>
      </NavBar>
    </Header>
    <div class="main">
      <div class="bg-first"></div>
      <div class="change-main">
        <div class="item" @click="fnOpenWin('account_security_change_password')">
          <div class="password-mobly">
            <img src="@/images/icon.passwordMobly.png" alt />
          </div>
          <div class="change-password">修改密码</div>
        </div>

        <div class="password-arrowhead-right">
          <img src="@/images/icon_arrowhead_right_gray.png" alt />
        </div>
      </div>
      <div class="bg-second"></div>
    </div>
  </div>
</template>

<script>
import Header from "@/components/header.vue";
import { NavBar } from "vant";
window.account_securityVue = {
  name: "account_security",
  components: { Header, NavBar },
  data() {
    return {};
  },
  methods: {
    fnOpenWin(name) {
      api.openWin({
        name: name,
        url: `${name}.html`,
        bgColor: "#fff",
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

export default window.account_securityVue;
</script>

<style lang="scss" scoped>
.back-btn {
  background: url(../images/icon_back.png) no-repeat left center;
  background-size: 9px 15px;
  padding: 22px;
}
.bg-first {
  background-color: #f8f8f8;
  width: 100%;
  height: 10px;
}

.change-main {
  width: 100%;
  height: 49px;
  display: flex;
  flex: 1;
  justify-content: space-between;
}

.item {
  display: flex;
  flex: 1;
}

.password-mobly img {
  width: 15px;
  height: 18px;
  margin: 16px 0 15px 14px;
}

.change-password {
  font-size: 13px;
  font-weight: 400;
  height: 12px;
  line-height: 49px;
  margin-left: 14px;
  color: rgba(22, 22, 22, 1);
}

.bg-second {
  background-color: #f8f8f8;
  width: 100%;
  height: 10px;
}

.password-arrowhead-right img {
  width: 6px;
  height: 10px;
  opacity: 0.42;
  margin: 20px 18px 19px 0;
}
</style>