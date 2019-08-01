<template>
  <div class="selected-container">
    <PullRefresh v-model="isLoading" @refresh="onRefresh">
      <List
        class="selected-list"
        v-model="loading"
        :finished="finished"
        finished-text="没有更多了"
        @load="onLoad"
        :offset="1000"
      >
        <div class="list-item" v-for="(item,index) in list" :key="index">
          <div class="m-information">
            <div class="u-title">{{item.article_title}}</div>
            <div class="m-info">
              <div class="time">{{item.publish_date}}</div>
              <div class="read">
                <i></i>
                {{item.article_click}}
              </div>
            </div>
          </div>
          <div class="m-pic">
            <img :src="item.article_image" alt />
          </div>
        </div>
      </List>
    </PullRefresh>
  </div>
</template>

<script>
import { List, PullRefresh } from "vant";

import axios from "axios";
import { setTimeout } from "timers";
window.information_selected_frmVue = {
  name: "information_selected_frm",
  components: { List, PullRefresh },
  data() {
    return {
      list: [],
      loading: false,
      finished: false,
      currentPage: 0,
      isLoading: false
    };
  },
  mounted() {},
  methods: {
    initList() {
      var vaules = {
        c: "asa",
        currentPage: this.currentPage,
        pageSize: 2
      };
      const formData = new FormData();
      Object.keys(vaules).forEach(key => {
        formData.append(key, vaules[key]);
      });

      axios.post(`http://clientapi.61lu.com/news/list`, formData).then(res => {
        if (res.data.code === 1) {
          this.isLoading = false;
          if (res.data.newsList && res.data.newsList.length > 0) {
            this.list = this.list.concat(res.data.newsList);
            this.loading = false;
          } else {
            this.loading = false;
            this.finished = true;
          }
        }
      });
    },
    onLoad() {
      setTimeout(() => {
        this.currentPage++;
        this.initList();
      }, 10);
    },
    onRefresh() {
      this.list = [];
      this.currentPage = 0;
      this.finished = false;
      setTimeout(() => {
        this.onLoad();
      }, 500);
    }
  }
};

export default window.information_selected_frmVue;
</script>

<style lang="scss" scoped>
.selected-container {
  padding: 0 14px;
  box-sizing: border-box;
  border-top: solid 10px #f7f7f7;
}

.selected-list {
  margin-top: 21px;
}

.selected-list .list-item {
  display: flex;
  margin-bottom: 29px;
}

.selected-list .m-information {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.selected-list .m-information .u-title {
  font-size: 14px;
  color: #161616;
  line-height: 22px;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;
  display: -webkit-box;
}

.selected-list .m-information .m-info {
  display: flex;
  justify-content: space-between;
  font-size: 11px;
  color: #999999;
}

.selected-list .m-information .read {
  font-size: 9px;
  vertical-align: middle;
}

.selected-list .m-information .read i {
  display: inline-block;
  width: 10px;
  height: 7px;
  background: url(../images/ddd.png);
  background-size: 100% 100%;
  margin-right: 3px;
}

.selected-list .m-pic {
  width: 102px;
  height: 68px;
  margin-left: 23px;
}

.selected-list .m-pic img {
  width: 102px;
  height: 68px;
}
</style>