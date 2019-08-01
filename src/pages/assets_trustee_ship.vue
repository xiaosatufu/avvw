<template>
  <div>
    <div class="deposit-show"></div>

    <div class="deposit-details">
      <div class="det money">
        <div class="text">托管电费</div>
        <div class="num">
          <div class="bold">
            0.25
            <span>元/度</span>
          </div>
        </div>
      </div>
      <div class="det min-num">
        <div class="text">最小托管数量</div>
        <div class="num">10 台</div>
      </div>
      <div class="det rest">
        <div class="text">剩余机位</div>
        <div class="num">5600 台</div>
      </div>
    </div>

    <div class="require">
      <div class="deposit-require">
        <p class="require-title">托管要求:</p>
        <p class="require-detail">预付一个月电费</p>
      </div>
      <div class="deposit-manage">
        <p class="manage-title">管理费:</p>
        <p class="manage-detail">0元/台/月</p>
      </div>
    </div>

    <div class="line"></div>
    <input type="hidden" class="hidden-box" id="hidden-box" />
    <div class="calculate">
      <div class="type">
        <p class="type-text">托管类型</p>
        <select class="select" id="select" onchange="changeValue()">
          <option value disabled selected hidden>请选择托管类型工号</option>
          <!-- <option value="" class="tip"></option> -->
          <option value="1.7">ASIC矿机--1.7kw/h</option>
          <option value="1.5">蚂蚁S9i--1.5kw/h</option>
          <option value="1.7">蚂蚁T9+--1.7kw/h</option>
          <option value="2.8">蚂蚁S17--2.8kw/h</option>
          <option value="1.8">蚂蚁T15--1.8kw/h</option>
          <option value="1.6">蚂蚁S11--1.6kw/h</option>
          <option value="2.3">芯动T2T--2.3kw/h</option>
          <option value="2.4">神马M10--2.4kw/h</option>
          <option value="2.3">神马M3--2.3kw/h</option>
        </select>
      </div>
      <div class="deposit-num">
        <p class="text">托管数量</p>
        <input
          type="text"
          class="input"
          id="num"
          oninput="changeValue()"
          placeholder="请输入托管数量"
          onkeyup="if(this.value.length==1){this.value=this.value.replace(/[^1-9]/g,'')}else{this.value=this.value.replace(/\D/g,'')}"
          onafterpaste="if(this.value.length==1){this.value=this.value.replace(/[^1-9]/g,'')}else{this.value=this.value.replace(/\D/g,'')}"
        />
      </div>
      <div class="pay">
        <p class="text">预付电费</p>
        <p class="pay-num" id="money">0</p>
        <span class="par-money">元</span>
      </div>
    </div>

    <div class="apply" onclick="displayDiv()" id="change-btn-color">
      <p class="allpy-text" id="deposit">申请托管</p>
    </div>

    <div class="footer">
      <img src="@/images/tips_icn.png" />
      <p class="notice">温馨提示:</p>
      <p class="notes">申请托管成功后，请联系客服进行托管</p>
    </div>

    <div class="foot-box">
      <div id="light" class="float-div">
        <span class="succes">托管申请提交成功</span>
        <span class="attack">请尽快联系客服，进行托管后续操作</span>
        <button class="button-click" onclick="displayfade()">确认</button>
      </div>
    </div>

    <div id="fade" class="black_overlay"></div>
  </div>
</template>

<script>
window.assets_trustee_shipVue = {
  name: "assets_trustee_ship",
  components: {},
  data() {
    return {};
  },
  methods: {}
};

export default window.assets_trustee_shipVue;
</script>

<style lang="scss" scoped>
.deposit-show {
  height: 110px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 15px 14px 21px 14px;
  background: url("../images/bg_02.png") no-repeat;
  background-size: 100% 100%;
}

.deposit-details {
  display: flex;
  height: 47px;
  margin: 0 17px 0 13px;
  justify-content: space-between;
  align-items: center;
}

.deposit-details .det {
  text-align: center;
}

.money .text {
  text-align: left;
}

.min-num {
  text-align: center;
}

.num {
  font-size: 12px;
  color: rgba(245, 131, 0, 1);
  margin-top: 16px;
}

.bold {
  font-size: 14px;
  font-weight: 400;
  color: rgba(245, 131, 0, 1);
}

.bold span {
  font-size: 12px;
  margin-bottom: 0px;
}

.require {
  height: 83px;
  position: relative;
  font-size: 12px;
  color: rgba(102, 102, 102, 1);
  margin-left: 14px;
  margin-top: 23px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.require .deposit-require::before {
  content: "";
  position: absolute;
  top: -50%;
  bottom: -50%;
  left: -50%;
  right: -50%;
  width: 200%;
  height: 200%;
  -webkit-transform: scale(0.5);
  transform: scale(0.5);
  border-top: solid 1px rgba(239, 239, 239, 1);
  box-sizing: border-box;
}

.require .deposit-require {
  flex-direction: row;
  display: flex;
  justify-content: flex-start;
}

.require .deposit-manage {
  flex-direction: row;
  display: flex;
  justify-content: flex-start;
}

.require-detail {
  margin-left: 8px;
}

.manage-detail {
  margin-left: 21px;
}

.line {
  height: 10px;
  background: rgba(247, 247, 247, 1);
}

.calculate {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.type {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  margin-left: 15px;
  line-height: 49px;
}

.type-text {
  width: 80px;
  font-size: 13px;
  color: rgba(22, 22, 22, 1);
}

.select {
  margin-left: 42px;
  width: 100%;
  border: 0;
  outline: none;
  background-color: white;
  font-size: 13px;
  color: #161616;
  -webkit-appearance: none;
  background: url(../images/icon_dropdown.png) no-repeat 90% 50%;
  background-size: 14px 10px;
  background-color: white;
}

.type option {
  color: black;
}

.type option {
  color: black;
}

.deposit-num {
  margin-left: 14px;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  height: 49px;
  line-height: 49px;
}

.deposit-num .text {
  font-size: 13px;
  color: rgba(22, 22, 22, 1);
}

.deposit-num .input {
  font-size: 13px;
  color: rgba(22, 22, 22, 1);
  outline: none;
  margin-left: 50px;
}

input::-webkit-input-placeholder {
  font-size: 12px;
  color: rgba(204, 204, 204, 1);
}

.pay {
  height: 49px;
  margin-left: 14px;
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  line-height: 49px;
}

.calculate > div {
  position: relative;
}

.calculate > div::after {
  content: "";
  width: 100%;
  height: 1px;
  background: #efefef;
  position: absolute;
  bottom: 0;
  left: 0;
  transform: scaleY(0.5);
}

.pay .text {
  font-size: 13px;
  color: rgba(22, 22, 22, 1);
}

.pay-num {
  font-size: 13px;
  color: rgba(22, 22, 22, 1);
  margin-left: 50px;
}

.par-money {
  font-size: 13px;
  color: rgba(22, 22, 22, 1);
}

.apply {
  height: 44px;
  background: rgba(255, 180, 117, 1);
  border-radius: 4px;
  margin: 24px 14px 0px 14px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.allpy-text {
  font-size: 14px;
  font-weight: 500;
  color: rgba(254, 254, 254, 1);
}

.footer {
  height: 84px;
  background: url("../images/deposit_bottom_bg.png") no-repeat;
  background-size: 100% 100%;
  margin: 15px 14px 41px 14px;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.footer img {
  width: 12px;
  height: 12px;
  position: absolute;
  top: 28px;
  left: 9px;
}

.footer .notice {
  font-size: 12px;
  color: rgba(252, 95, 96, 1);
  text-indent: 27px;
  margin-top: 23px;
}

.footer .notes {
  font-size: 12px;
  color: rgba(153, 153, 153, 1);
  text-indent: 11px;
  margin-bottom: 20px;
}

.succes {
  margin-top: 108px;
  font-size: 16px;
  color: rgba(22, 22, 22, 1);
}

.attack {
  margin-top: 16px;
  font-size: 13px;
  color: rgba(153, 153, 153, 1);
  line-height: 18px;
}

.button-click {
  width: 200px;
  height: 41px;
  background: rgba(255, 148, 61, 1);
  border-radius: 4px;
  font-size: 14px;
  color: rgba(254, 254, 254, 1);
  margin: 26px 6px 0 0;
}

.black_overlay {
  display: none;
  position: absolute;
  top: 0%;
  left: 0%;
  width: 100%;
  height: 120%;
  background-color: #696969;
  z-index: 1001;
  -moz-opacity: 0.8;
  opacity: 0.8;
  filter: alpha(opacity=88);
}

.foot-box {
  position: relative;
}

.det > .text {
  font-size: 11px;
  color: rgba(153, 153, 153, 1);
}

.float-div {
  width: 253px;
  height: 246px;
  border-radius: 4px;
  text-align: center;
  display: none;
  position: absolute;
  margin-top: -360px;
  background: url(../images/icon_circle_orenge.png) no-repeat;
  background-size: 66px 66px;
  background-position: 50% 21px;
  background-color: white;
  z-index: 1002;
  overflow: auto;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>