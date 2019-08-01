<template>
  <div>
    <div class="analyzer-container">
      <div class="analyzer-form">
        <ul>
          <li>
            <div class="u-label">
              <p>算力周期</p>
            </div>
            <div class="input-wrap">
              <select class="slect-wrap" id="day">
                <option value="30">30天</option>
                <option value="90">90天</option>
                <option value="180">180天</option>
              </select>
            </div>
          </li>
          <li>
            <div class="u-label">
              <p>算力数量</p>
            </div>
            <div class="input-wrap">
              <input
                type="text"
                id="portion"
                placeholder="请输入需要分析的算力数量(最大为99999)"
                maxlength="5"
                onkeyup="if(this.value.length==1){this.value=this.value.replace(/[^1-9]/g,'')}else{this.value=this.value.replace(/\D/g,'')}"
                onafterpaste="if(this.value.length==1){this.value=this.value.replace(/[^1-9]/g,'')}else{this.value=this.value.replace(/\D/g,'')}"
                oninput="changeBtnColor()"
              />
              <span>T</span>
            </div>
          </li>
          <li>
            <div class="u-label">
              <p>算力价格</p>
              <span>
                <em>其他费用:0元</em>
                <em>单份算力 · 1500元/T</em>
              </span>
            </div>
            <div class="input-wrap bg-color">
              <input type="text" id="deposit" readonly="“readonly”" value="1500" />
              <span>元 &nbsp;</span>
            </div>
          </li>
        </ul>
      </div>
      <div class="btn-analyzer" id="change-btn-color" onclick="count()">分析产出</div>
    </div>
    <div class="statistics-box">
      <div class="statistics-content">
        <div class="statistics-header">
          <div class="u-tt">算力产出统计</div>
          <!-- <div class="u-icon"></div> -->
        </div>
        <ul>
          <li>
            <div class="u-tt">每天产出(BTC)</div>
            <div class="u-btc" id="d_income">0.00321500</div>
            <div class="u-money">
              <span>&nbsp;≈</span>
              <span id="d_money">￥5.03</span>
            </div>
          </li>
          <li>
            <div class="u-tt">每月产出(BTC)</div>
            <div class="u-btc" id="m_income">0.09645000</div>
            <div class="u-money">
              <span>&nbsp;≈</span>
              <span id="m_money">￥150.30</span>
            </div>
          </li>
          <li>
            <div class="u-tt">每年产出(BTC)</div>
            <div class="u-btc" id="y_income">1.15740000</div>

            <div class="u-money">
              <span>&nbsp;≈</span>
              <span id="y_money">￥26140.60</span>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
window.quotation_analyzerVue = {
  name: "quotation_analyzer",
  components: {},
  data() {
    return {};
  },
  methods: {}
};

export default window.quotation_analyzerVue;
</script>

<style lang="scss" scoped>
@import "@/css/common.scss";
.analyzer-container {
  margin: 0 14px 20px;
}

.analyzer-form {
  margin: 20px 0;
  background: rgba(255, 255, 255, 1);
  box-shadow: 0px 0px 13px 0px rgba(197, 197, 197, 0.32);
  border-radius: 4px;
  padding: 25px 20px;
  box-sizing: border-box;
}

.analyzer-form .u-label {
  color: #161616;
  font-size: 13px;
  display: flex;
  justify-content: space-between;
}
.analyzer-form .u-label p {
  font-weight: 600;
}
.analyzer-form .u-label span {
  font-size: 10px;
  color: #f58220;
}

.analyzer-form .u-label span em:first-child {
  margin-right: 23px;
}

.analyzer-form .input-wrap {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 0;
  margin-bottom: 15px;
  position: relative;
}

.analyzer-form li:last-child .input-wrap {
  margin-bottom: 0;
}

.analyzer-form .input-wrap::after {
  content: "";
  width: 100%;
  height: 1px;
  background: #efefef;
  transform: scaleY(0.5);
  position: absolute;
  left: 0;
  bottom: 0;
}

.analyzer-form .input-wrap input {
  font-size: 14px;
  outline: none;
}

.analyzer-form .input-wrap span {
  font-size: 13px;
}

.analyzer-container .btn-analyzer {
  width: 100%;
  height: 44px;
  line-height: 44px;
  background: #ffb475;
  border-radius: 4px;
  text-align: center;
  color: #fff;
  font-size: 14px;
}

.statistics-box {
  position: relative;
}

.statistics-box::before {
  content: "";
  width: 100%;
  height: 1px;
  background: #efefef;
  transform: scaleY(0.5);
  position: absolute;
  top: 0;
  left: 0;
}

.statistics-content {
  margin: 0 14px;
  padding-top: 20px;
  position: relative;
}

.statistics-content::before,
.statistics-content::after {
  content: "";
  width: 8px;
  height: 8px;
  position: absolute;
  bottom: 0;
}

.statistics-content::before {
  background: url(../images/icon_label_01.png);
  background-size: 100% 100%;
  left: 0;
}

.statistics-content::after {
  background: url(../images/icon_label_02.png);
  background-size: 100% 100%;
  right: 0;
}

.statistics-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
}

.statistics-header .u-tt {
  font-size: 12px;
  color: rgba(22, 22, 22, 1);
}

/* .statistics-header .u-icon {
            width: 14px;
            height: 14px;
            background: url(../images/icon_question.png);
            background-size: 100% 100%;
        } */

.statistics-content ul {
  margin: 0 15px;
}

.statistics-content li {
  display: flex;
  align-items: center;
  padding-bottom: 16px;
}

.statistics-content li .u-tt {
  margin-right: 36px;
  font-size: 10px;
  color: #999;
}

.statistics-content li .u-tt {
  font-size: 10px;
  color: rgba(153, 153, 153, 1);
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  -o-text-overflow: ellipsis;
  overflow: hidden;
  word-break: keep-all;
}

.statistics-content li .u-btc {
  font-size: 12px;
  color: rgba(50, 50, 50, 1);
}

.statistics-content li .u-money {
  font-size: 12px;
  color: #f58220;
  white-space: nowrap;
  text-overflow: ellipsis;
  -o-text-overflow: ellipsis;
  overflow: hidden;
  word-break: keep-all;
}

.slect-wrap {
  width: 100%;
  outline: none;
  -webkit-appearance: none;
  border: 0;
  background: url(../images/icon_dropdown.png) no-repeat right center;
  background-size: 14px 10px;
  background-color: white;
}

#portion {
  width: 100%;
}

input::-webkit-input-placeholder {
  font-size: 12px;
}

.bg-color {
  background: rgba(247, 247, 247, 1);
  margin-top: 15px;
  height: 0px;
}

#deposit {
  text-indent: 6px;
}
</style>