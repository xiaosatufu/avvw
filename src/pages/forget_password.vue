<template>
  <div>
    <div class="login-container">
      <div class="u-tt">输入信息重新找回密码</div>
      <div class="login-form">
        <div class="u-label">
          <div class="label">手机号</div>
          <div class="code">+86</div>
        </div>
        <div class="input-wrap">
          <input
            type="text"
            id="mobile"
            placeholder="请输入手机号码"
            maxlength="11"
            oninput="changeBtnColor()"
          />
        </div>
        <div class="u-label">
          <div class="label">手机验证码</div>
        </div>
        <div class="input-wrap">
          <input
            type="text"
            id="verificationCode"
            maxlength="6"
            placeholder="请输入6位验证码"
            oninput="changeBtnColor()"
          />
          <button onclick="handleSendSms()" class="handleSend">发送验证码</button>
        </div>
        <div class="u-label">
          <div class="label">设置密码</div>
        </div>
        <div class="input-wrap">
          <input
            type="password"
            id="password"
            placeholder="请设置登录密码，含数字、字母"
            maxlength="11"
            oninput="changeBtnColor()"
          />
        </div>
        <div class="u-label">
          <div class="label">重复密码</div>
        </div>
        <div class="input-wrap">
          <input
            type="password"
            id="repassword"
            placeholder="请重复密码"
            maxlength="11"
            oninput="changeBtnColor()"
          />
        </div>
        <div class="u-btn" onclick="handleRegister()" id="handle-register">完成</div>
      </div>
    </div>
  </div>
</template>

<script>
window.forget_passwordVue = {
  name: "forget_password",
  components: {},
  data() {
    return {};
  },
  methods: {}
};

export default window.forget_passwordVue;
</script>

<style lang="scss" scoped>
@import "@/css/common.scss";
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
  flex: 1;
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
}
</style>