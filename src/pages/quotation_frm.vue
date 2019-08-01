<template>
  <div class="quotation-wrap">
    <div class="transaction-heat-wrap">
      <div class="m-heat">
        <em>市场交易热度</em>
        <span>{{}}</span>
      </div>
      <div class="m-yesterday">
        <em>昨日大涨今日表现</em>
        <span class="m-yesterday-num">{{}}</span>
      </div>
      <div class="m-progress">
        <div class="left-progress u-progress"></div>
        <div class="right-progress u-progress"></div>
        <ul>
          <li>市值前100</li>
          <li>市值前200</li>
        </ul>
      </div>
      <ul class="m-detail">
        <li>
          上涨
          <span>{{}}</span>
        </li>
        <li>
          下跌
          <span>{{}}</span>
        </li>
        <li>
          上涨
          <span>{{}}</span>
        </li>
        <li>
          下跌
          <span>{{}}</span>
        </li>
      </ul>
    </div>
    <div class="analyzer-wrap">
      <div class="analyzer-header" @click="fnOpenWin('quotation_analyzer')">产出分析器</div>
      <ul class="m-analyzer">
        <li>
          <div class="u-tt">总市值</div>
          <div class="u-money">￥{{}}</div>
          <div class="u-percent">{{}}</div>
        </li>
        <li>
          <div class="u-tt">24H成交额</div>
          <div class="u-money">￥{{}}</div>
          <div class="u-percent">{{}}</div>
        </li>
        <li>
          <div class="u-tt">BTC价格</div>
          <div class="u-money">￥{{}}</div>
          <div class="u-percent">{{}}</div>
        </li>
      </ul>
    </div>
    <div class="exchange-wrap">
      <div class="u-title">交易所行情</div>
      <div class="exchange-nav">
        <div class="item">交易所</div>
        <div class="item">价格</div>
        <div class="item">24H涨跌幅</div>
      </div>
      <ul id="coin_data_list">
        <li>
          <div class="exchange-name">
            <div class="u-logo">
              <img src alt />
            </div>
            <div class="u-name">{{}}</div>
          </div>
          <div class="exchange-price">￥{{}}</div>
          <div class="exchange-percent">{{}}</div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
window.quotation_frmVue = {
  name: "quotation_frm",
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

export default window.quotation_frmVue;
</script>

<style lang="scss" scoped>
@import "@/css/common.scss";
.transaction-heat-wrap {
  background: #fff;
  margin: 44px 14px 10px;
  position: relative;
  padding: 19px 14px;
  box-sizing: border-box;
}

.transaction-heat-wrap .m-heat > em {
  color: #161616;
  font-size: 12px;
  vertical-align: top;
}

.transaction-heat-wrap .m-heat > span {
  font-size: 19px;
  color: #f58220;
  position: relative;
  top: -3px;
  left: 20px;
}

.transaction-heat-wrap .m-yesterday {
  /* display: flex; */
  /* margin-top: 8px; */
  margin-bottom: 12px;
}

.transaction-heat-wrap .m-yesterday > em {
  font-size: 10px;
  color: #999999;
}

.transaction-heat-wrap .m-yesterday > span {
  font-size: 11px;
  color: #f58220;
  background: rgba(245, 130, 32, 0.16);
  margin-left: 18px;
}

.transaction-heat-wrap .m-detail {
  display: flex;
  margin-top: 17px;
}

.transaction-heat-wrap .m-detail > li {
  font-size: 10px;
  color: #999;
  flex: 1;
  text-align: center;
}

.transaction-heat-wrap .m-detail span {
  font-size: 13px;
  color: #161616;
  margin-left: 7px;
}

.transaction-heat-wrap .m-progress {
  position: relative;
}

.transaction-heat-wrap .m-progress ul {
  display: flex;
  justify-content: space-between;
  padding-top: 13px;
}

.transaction-heat-wrap .m-progress li {
  font-size: 10px;
  color: #f58220;
  opacity: 0.56;
}

.transaction-heat-wrap .m-progress li:first-child {
  color: #55bd9a;
}

.transaction-heat-wrap .m-progress .u-progress {
  height: 5px;
  position: absolute;
  top: 0;
  width: 48%;
}

.transaction-heat-wrap .m-progress .left-progress {
  left: 0;
  background: linear-gradient(
    90deg,
    rgba(85, 189, 154, 1) 0%,
    rgba(80, 212, 90, 1) 100%
  );
}

.transaction-heat-wrap .m-progress .right-progress {
  right: 0;
  background: linear-gradient(
    90deg,
    rgba(245, 130, 32, 1) 0%,
    rgba(255, 106, 66, 1) 100%
  );
}

.transaction-heat-wrap .m-progress .left-progress::after {
  content: "";
  width: 0;
  height: 0;
  border-top: 5px solid transparent;
  border-bottom: 5px solid transparent;
  border-left: 5px solid #50d45a;
  position: absolute;
  right: -3px;
  top: -2.6px;
  z-index: 1;
  transform: rotate(90deg) scale(0.8);
}

.transaction-heat-wrap .m-progress .right-progress::after {
  content: "";
  width: 0;
  height: 0;
  border-top: 5px solid transparent;
  border-bottom: 5px solid transparent;
  border-left: 5px solid #f68121;
  position: absolute;
  left: -3px;
  top: -2.5px;
  z-index: 1;
  transform: rotate(270deg) scale(0.9);
}

.transaction-heat-wrap::after {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  z-index: 1;
  width: 200%;
  height: 200%;
  border: 1px solid #f0f0f0;
  -webkit-transform-origin: 0 0;
  transform-origin: 0 0;
  -webkit-transform: scale(0.5, 0.5);
  transform: scale(0.5, 0.5);
  /* border-radius: 10px; */
}

.analyzer-wrap {
  background: #fff;
  border: 1px solid rgba(240, 240, 240, 1);
  margin: 0 14px 10px;
}

.analyzer-header {
  height: 40px;
  line-height: 40px;
  position: relative;
  color: #161616;
  font-size: 12px;
  text-indent: 14px;
}

.analyzer-header::after {
  content: "";
  width: 5px;
  height: 8px;
  background: url(../images/icon_right_arrow.png);
  background-size: 100% 100%;
  position: absolute;
  right: 14px;
  top: 16px;
}

.analyzer-wrap .m-analyzer {
  position: relative;
  display: flex;
  /* justify-content: space-between; */
  text-align: center;
}

.analyzer-wrap .m-analyzer::before {
  content: "";
  width: 100%;
  height: 1px;
  background: #f0f0f0;
  transform: scaleY(0.5);
  position: absolute;
  top: 0;
  left: 0;
}

.analyzer-wrap .m-analyzer > li {
  flex: 1;
  position: relative;
  padding: 23px 0 22px 0;
}

.analyzer-wrap .m-analyzer > li .u-tt {
  color: #999;
  font-size: 10px;
}

.analyzer-wrap .m-analyzer > li .u-money {
  color: #161616;
  font-size: 14px;
  margin: 16px 0 10px 0;
  text-align: center;
  font-weight: 500;
}

.analyzer-wrap .m-analyzer > li .u-percent {
  color: #54c389;
  font-size: 10px;
}

.analyzer-wrap .m-analyzer > li:nth-child(2)::before {
  content: "";
  position: absolute;
  left: 0;
  bottom: 0;
  width: 1px;
  height: 100%;
  background-color: #f0f0f0;
  -webkit-transform: scaleX(0.5);
  transform: scaleX(0.5);
}

.analyzer-wrap .m-analyzer > li:nth-child(2)::after {
  content: "";
  position: absolute;
  right: 0;
  bottom: 0;
  width: 1px;
  height: 100%;
  background-color: #f0f0f0;
  -webkit-transform: scaleX(0.5);
  transform: scaleX(0.5);
}

.exchange-wrap {
  background: #fff;
}

.exchange-wrap .u-title {
  font-size: 13px;
  color: #161616;
  height: 40px;
  line-height: 40px;
  text-indent: 14px;
  position: relative;
}

/* .exchange-wrap .u-title span {
            display: inline;
        } */
.exchange-wrap .u-title::after {
  content: "";
  width: 100%;
  height: 1px;
  background: #f0f0f0;
  transform: scaleY(0.5);
  left: 0;
  bottom: 0;
  position: absolute;
}

.exchange-wrap .u-title::before {
  content: "";
  width: 20px;
  height: 1px;
  background: #ffb576;
  position: absolute;
  bottom: 1px;
  left: 38px;
}

.exchange-wrap .exchange-nav {
  height: 27px;
  margin: 12px 16px 21px;
  background: rgba(255, 255, 255, 1);
  box-shadow: 0px 0px 7px 0px rgba(197, 197, 197, 0.28);
  display: flex;
  /* justify-content: space-between; */
  padding: 0 8px;
  box-sizing: border-box;
  height: 27px;
  line-height: 27px;
  color: rgba(153, 153, 153, 1);
  opacity: 0.56;
  font-size: 10px;
}

.exchange-wrap .exchange-nav .item {
  flex: 1;
  text-align: center;
}

.exchange-wrap .exchange-nav .item:first-child {
  text-align: left;
}

.exchange-wrap .exchange-nav .item:last-child {
  text-align: right;
}

.exchange-wrap ul {
  margin: 0 16px;
  padding-bottom: 1px;
}

.exchange-wrap li {
  display: flex;

  /* justify-content: space-between; */
  font-size: 14px;
  margin-bottom: 32px;
}

.exchange-wrap li > div {
  flex: 1;
  text-align: center;
}

.exchange-wrap .exchange-name {
  display: flex;
  align-items: center;
}

.exchange-wrap .exchange-name .u-name {
  margin-left: 10px;
  color: #161616;
  font-weight: 500;
}

.exchange-wrap .exchange-name img {
  width: 20px;
  height: 20px;
}

.exchange-wrap .exchange-price {
  color: #161616;
}

.exchange-wrap .exchange-percent {
  text-align: right;
  color: #54c389;
}

.m-yesterday-num {
  padding: 2px;
}
</style>