<template>
  <div>
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
window.account_securityVue = {
  name: "account_security",
  components: {},
  data() {
    return {};
  },
  methods: {
    fnOpenWin(name) {
      api.openWin({
        name: name,
        url: `${name}.html`,
        bgColor: "#fff"
      });
    }
  }
};

export default window.account_securityVue;
</script>

<style lang="scss" scoped>
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