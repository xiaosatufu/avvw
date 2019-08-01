<template>
  <div>
    <div class="main">
      <div class="old-password input-warp">
        <p>原密码</p>
        <input
          type="password"
          id="old-password"
          placeholder="请输入原密码，限数字、字母"
          oninput="changeBtnColor()"
        />
      </div>
      <div class="new-password input-warp">
        <p>新密码</p>
        <input type="password" id="password" placeholder="请输入新密码，限数字、字母" oninput="changeBtnColor()" />
      </div>
      <div class="repeat-new-password input-warp">
        <p>重复密码</p>
        <input type="password" id="repassword" placeholder="请输入重复密码" oninput="changeBtnColor()" />
      </div>
      <div class="btn-submit">
        <button onclick="resetPassword()" id="reset-password">提交</button>
      </div>
    </div>
  </div>
</template>

<script>
window.account_security_change_passwordVue = {
  name: "account_security_change_password",
  components: {},
  data() {
    return {};
  },
  methods: {}
};

export default window.account_security_change_passwordVue;
</script>

<style lang="scss" scoped>
.main {
  display: flex;
  flex-direction: column;
  margin: 0 14px 0 13px;
}

.main p {
  height: 13px;
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
}
</style>