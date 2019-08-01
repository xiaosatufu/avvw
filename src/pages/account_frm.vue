<template>
  <div>
    <header class="header" id="loginStatus" tapmode @click="fnOpenWin('account_personal_data')">
      <div class="header_left">
        <img src="@/images/icon_avatar.png" alt />
        <div class="header_left_main">
          <div class="person_name">MobieUser</div>
          <div class="person_number">ID:{{}}</div>
        </div>
      </div>
      <div class="header_right">
        <img src="@/images/icon_arrowhead_right_gray.png" alt />
      </div>
    </header>
    <div class="main">
      <p>请勿透露密码、短信验证码给任何人，包括易挖工作人员。</p>
    </div>
    <div id="footer" class="footer" @click="fnOpenWin('account_security')">
      <div class="item">
        <div class="footer-shield">
          <img src="@/images/icon_shield.png" alt />
        </div>
        <div class="footer-security">账户安全</div>
      </div>
      <div class="footer-right">
        <img src="@/images/icon_arrowhead_right_gray.png" alt />
      </div>
    </div>
    <div style="width: 100%;height:10px;background-color:#F8F8F8;"></div>

    <header class="not-login header" id="unloginStatus">
      <div class="header_left">
        <div class="u-tt">欢迎来到易挖</div>
        <p>挖掘数字金矿 易享未来财富</p>
      </div>
      <div class="header_right" @click="fnOpenWin('login_account')">登录/注册</div>
    </header>
    <div class="main">
      <p>请勿透露密码、短信验证码给任何人，包括易挖工作人员。</p>
    </div>
  </div>
</template>

<script>
window.account_frmVue = {
  name: "account_frm",
  components: {},
  data() {
    return {};
  },
  methods: {
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

export default window.account_frmVue;
</script>

<style lang="scss" scoped>
.header {
  display: flex;
  justify-content: space-between;
  /* height: 46px; */
  align-items: center;
  padding: 0 19px 0 14px;
  box-sizing: border-box;
  margin-bottom: 19px;
  margin-top: 44px;
}

.header_left {
  display: flex;
  flex: 1;
}

.header_left_main {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.header_left img {
  height: 46px;
  width: 46px;
  margin-right: 13px;
  /* margin: 0 0 19px 14px; */
}

.not-login .header_left {
  display: block;
}

.not-login .header_left .u-tt {
  font-size: 16px;
  color: #323232;
  margin-bottom: 9px;
}

.not-login .header_left p {
  font-size: 12px;
  color: #999;
}

.not-login .header_right {
  width: 88px;
  height: 32px;
  background: rgba(246, 141, 56, 1);
  border-radius: 4px;
  font-size: 13px;
  color: #fff;
  text-align: center;
  line-height: 32px;
}

.person_name {
  font-size: 18px;
  font-weight: 400;
  color: rgba(50, 50, 50, 1);
  /* margin: 4px 0 0 13px; */
}

.person_number {
  font-size: 12px;
  font-weight: 400;
  color: rgba(153, 153, 153, 1);
  /* margin: 0 0 29px 13px; */
}

.header_right img {
  height: 11px;
  width: 6px;
  /* margin: 18px 19px 37px 0; */
}

.main {
  width: 100%;
  height: 28px;
  background: rgba(248, 248, 248, 1);
}

.main p {
  font-size: 11px;
  color: #9d9b99;
  opacity: 0.68;
  line-height: 28px;
  margin-left: 14px;
}

.footer {
  width: 100%;
  height: 50px;
  display: flex;
  flex: 1;
  justify-content: space-between;
  align-items: center;

  padding: 0 19px 0 14px;
  box-sizing: border-box;
}

.item {
  display: flex;
  flex: 1;
  align-items: center;
}

.footer-shield img {
  width: 15px;
  height: 19px;
  margin-right: 13px;
  /* margin: 17px 13px 15px 19px; */
}

.footer-security {
  font-size: 13px;
  font-weight: 400;
  color: rgba(22, 22, 22, 1);
  line-height: 50px;
}

.footer-right img {
  width: 6px;
  height: 11px;
  /* margin: 20px 19px 20px 0; */
}
</style>