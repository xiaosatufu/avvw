<template>
  <div>
    <div class="cost-bg">
      <div class="cost-usable">
        <div class="usable-text">可用额度(元)</div>
        <div class="usable-num">
          150000000.
          <span class="small-num">47</span>
        </div>
      </div>
      <div class="cost-value">
        <div class="value-text">矿机价值(元)</div>
        <div class="value-num">
          6000.
          <span class="small-num">00</span>
        </div>
        <div class="value-note">· 用于支付托管, 暂时冻结</div>
      </div>
    </div>
    <div class="recharch" onclick="hancleCharge()">充值</div>
    <div class="line"></div>
    <div class="doing">处理中订单</div>
    <div class="doing-order">暂无数据</div>
  </div>
</template>

<script>
window.assets_cost_centerVue = {
  name: "assets_cost_center",
  components: {},
  data() {
    return {};
  },
  methods: {}
};

export default window.assets_cost_centerVue;
</script>

<style lang="scss" scoped>
.header::after {
  content: "";
  width: 100%;
  height: 1px;
  background: #dbdbdb;
  transform: scaleY(0.5);
  position: absolute;
  left: 0;
  bottom: 0;
}

.back {
  width: 9px;
  height: 15px;
  background: url(../images/icon_back.png) no-repeat center;
  background-size: 9px 15px;
  box-sizing: border-box;
  position: absolute;
  /* bottom: 15px; */
  padding: 22px;
}

/* .back img {
            left: 17px;
            top: 15px;
            height: 15px;
            width: 9px;
            color: rgba(14, 14, 14, 1);
            position: absolute;
        } */

.cost-bg {
  display: flex;
  /* height: 146px; */
  justify-content: space-around;
  margin: 30px 15px;
}

.cost-bg .cost-usable {
  width: 154px;
  height: 93px;
  background: #ff9136;
  box-shadow: 0 15px 30px RGBA(255, 145, 54, 0.3);
  border-radius: 5px;
  padding-left: 20px;
  box-sizing: border-box;
  /* margin-top: 18px; */
  /* margin-left: 17px; */
  /* height: 108px; */
  /* width: 169px; */
  /* background: url("./cost_usable_bg.png") no-repeat; */
  /* background-size: 169px 108px; */
}

.cost-bg .cost-usable .usable-text {
  /* height: 10px; */
  font-size: 10px;
  color: rgba(255, 255, 255, 1);
  opacity: 0.86;
  padding: 22px 0 10px 0;
  /* margin-top: 29px; */
  /* margin-left: 26px; */
}

.cost-bg .cost-usable .usable-num {
  font-size: 18px;
  color: rgba(255, 255, 255, 1);
  /* margin-top: 12px; */
  /* margin-left: 26px; */
  /* display: flex; */
}

.cost-bg .cost-value {
  width: 154px;
  height: 93px;
  background: #fff;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
  border-radius: 5px;
  padding-left: 20px;
  box-sizing: border-box;
  /* margin: 13px 13px 0 0; */
  /* background: url("./cost_value_bg.png") no-repeat; */
  /* background-size: 177px 116px; */
}

.cost-bg .cost-value .value-text {
  /* height: 10px; */
  font-size: 10px;
  color: rgba(50, 50, 50, 1);
  opacity: 0.68;
  padding: 22px 0 10px 0;
  /* margin-top: 34px; */
  /* margin-left: 30px; */
}

.cost-bg .cost-value .value-num {
  /* height: 13px; */
  font-size: 18px;
  font-weight: 400;
  color: rgba(50, 50, 50, 1);
  margin-top: 1px;
  /* margin-left: 30px; */
  /* display: flex; */
}

.cost-bg .cost-value .value-note {
  font-size: 9px;
  color: rgba(255, 210, 173, 1);
  line-height: 12px;
  margin-top: 5px;
  /* margin-top: 10px; */
  /* margin-left: 30px; */
}

.small-num {
  font-size: 9px;
  margin-top: 6px;
}

.recharch {
  height: 42px;
  background: rgba(246, 129, 33, 1);
  box-shadow: 0px 0px 8px 0px rgba(246, 129, 33, 0.4);
  border-radius: 4px;
  font-size: 14px;
  font-weight: 500;
  color: rgba(254, 254, 254, 1);
  line-height: 42px;
  letter-spacing: 2px;
  text-align: center;
  margin: 0 15px;
  margin-top: 10px;
}

.line {
  height: 10px;
  background: rgba(247, 247, 247, 1);
  margin: 39px 0 0 0;
}

.doing {
  font-size: 13px;
  font-weight: 600;
  color: rgba(50, 50, 50, 1);
  line-height: 35px;
  margin-top: 24px;
  margin-left: 16px;
}

.doing-order {
  font-size: 12px;
  color: rgba(153, 153, 153, 1);
  line-height: 35px;
  opacity: 0.56;
  margin-top: 44px;
  text-align: center;
}
</style>