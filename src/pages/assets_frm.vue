<template>
  <div class="assets-container">
    <div class="m-not-login">
      <div class="u-icon"></div>
      <p>请先登录</p>
      <button @click="fnOpenLoginAccount">立即登录</button>
    </div>

    <div class="content">
      <div class="property-main">
        <div class="property-main-yesterday">
          <div class="u-title">昨日产出(BTC)</div>
          <div class="u-btc">
            {{}}
            <span>≈ ￥{{}}</span>
          </div>
        </div>
        <div class="property-main-today">
          <div class="today">
            <div class="u-tt">今日已挖(BTC)</div>
            <p id="totalBtc">0.00000000</p>
          </div>
          <div class="money">
            <div class="u-tt">算力金额(元)</div>
            <p>{{}}</p>
          </div>
        </div>
      </div>
      <div class="money-centent">
        <div class="show">费用中心</div>
        <div class="look" @click="fnOpenWin('assets_cost_center')">去查看</div>
      </div>

      <div class="swiper-container">
        <div class="swiper-wrapper">
          <div class="swiper-slide">
            <img src="@/images/activity_img01@3x.png" />
          </div>
          <div class="swiper-slide">
            <img src="@/images/activity_img02@3x.png" />
          </div>
        </div>
      </div>
      <div class="swiper-pagination"></div>
    </div>

    <div class="line">
      <p class="text">工具及服务</p>
    </div>
    <div class="service">
      <div class="sit deposit" @click="fnOpenWin('assets_trustee_ship')">
        <img src="@/images/deposit_icn@3x.png" />
        <p>托管服务</p>
      </div>
      <div class="sit custService" @click="fnOpenWin('assets_order_detail_list')">
        <img src="@/images/order_icn@3x.png" />
        <p>订单明细</p>
      </div>
      <div class="sit order">
        <img src="@/images/custService_icn@3x.png" />
        <p>客服服务</p>
      </div>
    </div>
  </div>
</template>

<script>
window.assets_frmVue = {
  name: "assets_frm",
  components: {},
  data() {
    return {};
  },
  methods: {
    fnOpenWin(name) {
      api.openWin({
        name: name,
        url: `${name}.html`,
        bgColor:'#fff'
      });
    }
  }
};

export default window.assets_frmVue;
</script>

<style lang="scss" scoped>
header {
  height: 44px;
  font-size: 15px;
  text-align: center;
  line-height: 44px;
  /* position: fixed; */
  top: 0;
  left: 0;
  width: 100%;
  z-index: 10;
  background: #fff;
}

.content {
  margin: 0 14px 0;
}

.property-main {
  /* height: 139px; */
  background: linear-gradient(
    90deg,
    rgba(245, 102, 32, 1) 0%,
    rgba(245, 130, 32, 1) 100%
  );
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-bottom: 24px;
}

.property-main-yesterday {
  /* height: 82px; */
  position: relative;
  padding-left: 11px;
  box-sizing: border-box;
  margin-bottom: 20px;
}

.property-main-yesterday .u-title {
  font-size: 10px;
  color: rgba(255, 255, 255, 1);
  opacity: 0.68;
  padding: 20px 0 10px 0;
  position: relative;
  /* position: absolute;
            top: 21px;
            left: 13px; */
}

.property-main-yesterday .u-title::after {
  content: "";
  width: 11px;
  height: 8px;
  /* background: url(../images/hide_icn.png); */
  position: absolute;
  background-size: 100% 100%;
  margin-left: 13px;
  margin-top: 5px;
}

.property-main-yesterday .u-btc {
  font-size: 21px;
  color: rgba(255, 255, 255, 1);
  /* position: absolute;
            top: 46px;
            left: 11px; */
}

.property-main-yesterday .u-btc span {
  font-size: 12px;
  opacity: 0.82;
  margin-left: 20px;
}

.property-main-yesterday img {
  display: block;
  background-repeat: no-repeat;
  margin-left: 13px;
  width: 11px;
  height: 8px;
}

.property-main-today {
  display: flex;
  position: relative;
  flex: 1;
  align-items: center;
  background: rgba(255, 255, 255, 0.1);
  padding: 14px 0;
}

.property-main-today div {
  flex: 1;
  text-indent: 12px;
}

.property-main-today div .u-tt {
  position: relative;
  z-index: 1;
  font-size: 10px;
  color: rgba(255, 255, 255, 1);
  opacity: 0.68;
  margin-bottom: 7px;
}

.property-main-today div p {
  position: relative;
  z-index: 1;
  font-size: 14px;
  color: rgba(255, 255, 255, 1);
}

.money-centent {
  align-items: center;
  display: flex;
  position: relative;
  justify-content: space-between;
}

.money-centent .show {
  font-size: 13px;
  color: rgba(22, 22, 22, 1);
}

.money-centent .look {
  width: 64px;
  height: 29px;
  text-align: center;
  line-height: 29px;
  font-size: 13px;
  border-radius: 4px;
  color: rgba(255, 255, 255, 1);
  background: rgba(246, 141, 56, 1);
}

.swiper-slide {
  height: 95px;
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: flex-end;
}

.swiper-slide img {
  height: 82px;
  flex: 1;
  margin: 0px 7px 10px 7px;
}

.swiper-pagination-bullet .swiper-pagination-bullet-active {
  width: 10px;
  height: 3px;
  background: rgba(255, 226, 202, 1);
  border-radius: 1px;
}

.swiper-pagination {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 1px;
  margin-bottom: 12px;
  margin: auto;
  left: 0;
  right: 0;
  /* top: -10px; */
  margin-top: -10px;
}

.swiper-pagination-bullet {
  width: 10px;
  height: 3px;
  background: rgba(233, 233, 233, 1);
  border-radius: 1px;
  margin: 0 4px;
}

.swiper-pagination-bullet-active {
  background: rgba(255, 226, 202, 1);
}
.swiper-container {
  padding-bottom: 20px;
  position: relative;
}

.line {
  height: 28px;
  line-height: 28px;
  background: rgba(247, 247, 247, 1);
  font-size: 11px;
  color: #9d9b99;
  text-indent: 15px;
}

.service {
  display: flex;
  height: 93px;
}

.service .sit {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.service img {
  width: 11px;
  height: 12px;
}

.service p {
  font-size: 12px;
  font-weight: 500;
  color: rgba(22, 22, 22, 1);
  opacity: 0.68;
  margin-top: 11px;
}

.custService {
  position: relative;
}

.custService::before {
  content: "";
  width: 1px;
  height: 30px;
  background: rgba(240, 240, 240, 1);
  position: absolute;
  left: 0px;
  top: 34px;
}

.custService::after {
  content: "";
  height: 30px;
  border-right: 1px solid rgba(240, 240, 240, 1);
  position: absolute;
  top: 34px;
  right: 0;
}

.m-not-login {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
  height: 80vh;
}

.m-not-login .u-icon {
  width: 108px;
  height: 81px;
  background: url(../images/icon_empty.png) no-repeat;
  background-size: 108px 81px;
}

.m-not-login p {
  color: #999;
  font-size: 14px;
  margin: 30px 0;
}

.m-not-login button {
  width: 136px;
  height: 40px;
  background: rgba(246, 141, 56, 1);
  border-radius: 4px;
  color: #fff;
  font-size: 14px;
  border: none;
}
</style>