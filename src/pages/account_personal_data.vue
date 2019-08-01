<template>
  <div>
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
    <button class="btn-logout" onclick="rmStorage()">退出登录</button>
  </div>
</template>

<script>
window.account_personal_dataVue = {
  name: "account_personal_data",
  components: {},
  data() {
    return {};
  },
  methods: {}
};

export default window.account_personal_dataVue;
</script>

<style lang="scss" scoped>
body {
  background: #f8f8f8;
  height: 100vh;
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