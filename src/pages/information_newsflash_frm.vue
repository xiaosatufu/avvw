<template>
  <div>
    <div class="newsflash-container">
      <PullRefresh v-model="isLoading" @refresh="onRefresh">
        <List
          v-model="loading"
          :finished="finished"
          finished-text="没有更多了"
          @load="onLoad"
          :offset="1000"
        >
          <IndexBar :index-list="indexList">
            <!-- <template v-for="(item,index) in list" :key="index"> -->

            <!-- </template> -->
            <div v-for="(item,index) in list" :key="index">
              <IndexAnchor index="1">{{list[index].publish_date}}</IndexAnchor>
              <div class="list-item">1111111111</div>
              <div class="list-item">1111111111</div>
              <div class="list-item">1111111111</div>
              <div class="list-item">1111111111</div>
              <div class="list-item">1111111111</div>
            </div>
          </IndexBar>
        </List>
      </PullRefresh>
    </div>
  </div>
</template>

<script>
import { IndexBar, List, IndexAnchor, PullRefresh } from "vant";
import axios from "axios";
window.information_newsflash_frmVue = {
  name: "information_newsflash_frm",
  components: { IndexBar, IndexAnchor, List, PullRefresh },
  data() {
    return {
      indexList: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
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
        c: "new",
        currentPage: this.currentPage
      };
      const formData = new FormData();
      Object.keys(vaules).forEach(key => {
        formData.append(key, vaules[key]);
      });
      var record = [
        // {
        //   date: "1111",
        //   data: []
        // },
        // {
        //   date: "1111",
        //   data: []
        // }
      ];

      axios.post(`http://clientapi.61lu.com/news/list`, formData).then(res => {
        if (res.data.code === 1) {
          this.isLoading = false;
          if (res.data.newsList && res.data.newsList.length > 0) {
            // this.list = this.list.concat(res.data.newsList);

            // res.data.newsList.map((item,index)=>{
            //   console.log(item)
            //   if (item.publish_date) {

            //   }
            // })

            

            // res.data.newsList.forEach((val, index) => {
            //   ["publish_date"].forEach((type, j) => {
            //     console.log(record[j].date);
            //     if (record[j].date === val[type]) {
            //       record[j].date = val
            //     } else {
            //       record[j].data = val
            //     }
            //     // if (record[index].date==val[type]) {
            //     //   record[index].date = val[type]
            //     //   record[index].data = val
            //     //   // record[val[type]].push(val);
            //     // } else {

            //     //   record[index].data = val
            //     //   // record[val[type]] = [val];
            //     // }
            //   });
            // });

            this.list = record;
            console.log(this.list);
            // console.log(this.list.length);
            // for (let i = 0; i < this.list.length; i++) {
            //   console.log(this.list[i]);
            // }

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

export default window.information_newsflash_frmVue;
</script>

<style lang="scss" scoped>
.newsflash-container {
  overflow: hidden;
  position: relative;
  background: #fff;
  z-index: 2;
}

.newsflash-wrap {
  position: relative;
}

.newsflash-wrap .u-date {
  width: 100%;
  height: 36px;
  line-height: 36px;
  background: #f8f8f8;
  text-indent: 15px;
  color: #999;
  font-size: 11px;
  margin-bottom: 6px;
}

.newsflash-wrap .u-date.fixed {
  position: fixed;
  top: 0;
  left: 0;
  background: #fff;
}

.newsflash-wrap ul {
  margin: 0 25px;
  position: relative;
}

.newsflash-wrap li {
  position: relative;
}

.newsflash-wrap ul::after {
  content: "";
  width: 1px;
  height: 200%;
  position: absolute;
  background: #f1f1f1;
  top: 5px;
  left: -8px;
}

.newsflash-wrap .u-time {
  color: #999;
  font-size: 11px;
  margin-bottom: 10px;
  position: relative;
}

.newsflash-wrap .u-time::before {
  content: "";
  width: 5px;
  height: 5px;
  border: solid 1.5px #9ca5a8;
  box-sizing: border-box;
  position: absolute;
  border-radius: 100%;
  top: 50%;
  margin-top: -2.5px;
  margin-right: -8px;
  left: -10px;
  z-index: 1;
}

.newsflash-wrap .u-tt {
  color: #161616;
  font-size: 14px;
  font-weight: 700;
  margin-bottom: 13px;
}

.newsflash-wrap .u-intro {
  font-size: 14px;
  line-height: 24px;
  /* margin-bottom: 20px; */
}

.newsflash-wrap .u-intro img {
  display: block;
  max-width: 100%;
}

.newsflash-wrap .m-btns {
  display: flex;
  justify-content: space-between;
  padding-bottom: 30px;
  margin-top: 20px;
  font-size: 11px;
  color: #999;
}

.newsflash-wrap .m-btns .u-hot i {
  width: 11px;
  height: 11px;
  background: url(../images/heat_icn@3x.png);
  background-size: 100% 100%;
  display: inline-block;
  position: relative;
  top: 1px;
}

.newsflash-wrap .m-btns .u-share i {
  width: 11px;
  height: 11px;
  background: url(../images/icon_share.png);
  background-size: 100% 100%;
  display: inline-block;
  position: relative;
  top: 1px;
  margin-right: 4px;
}
</style>