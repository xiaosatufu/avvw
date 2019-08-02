<template>
  <div>
    <Header></Header>
    <Footer @changeTab="handleChangeTab"></Footer>
    <!-- <Tabbar
      v-model="tabActive"
      active-color="#F68121"
      inactive-color="#C2C0BE"
      id="tabbar"
      @change="changeTab"
      fixed
    >
      <TabbarItem>
        <span>资讯</span>
        <img slot="icon" slot-scope="props" :src="props.active ? icon[0].active : icon[0].normal" />
      </TabbarItem>
      <TabbarItem>
        <span>行情</span>
        <img slot="icon" slot-scope="props" :src="props.active ? icon[1].active : icon[1].normal" />
      </TabbarItem>
      <TabbarItem>
        <span>资产</span>
        <img slot="icon" slot-scope="props" :src="props.active ? icon[2].active : icon[2].normal" />
      </TabbarItem>
      <TabbarItem>
        <span>我</span>
        <img slot="icon" slot-scope="props" :src="props.active ? icon[3].active : icon[3].normal" />
      </TabbarItem>
    </Tabbar>-->
  </div>
</template>

<script>
import Header from "@/components/header.vue";
import Footer from "@/components/footer.vue";
import apicloud from "@/libs/apicloud";

window.homeVue = {
  name: "home",
  components: { Footer, Header },
  data() {
    return {
      frameHeight: 0,
      headerHeight: 0,
      footerHeight: 0
    };
  },
  mounted() {
    // $api.fixTabBar($api.byId("tabbar"));
    // apicloud.fixTabBar(apicloud.dom("#tabbar")); // Fix the APP header bug

    // console.log(11)
    // No vue-router, use apicloud's framegroup to get the max transform efficiency
    // But if u wanna a smooth coding feeling, just use the vue router and the v-tap
    this.headerHeight = apicloud.dom("#header").offsetHeight;

    let footerHeight = apicloud.dom("#tabbar").offsetHeight;

    this.frameHeight = this.$ac.winHeight - this.headerHeight - footerHeight;

    window.localStorage.setItem(
      "view",
      JSON.stringify({
        headerHeight: this.headerHeight,
        frameHeight: this.frameHeight
      })
    );

    alert("home" + window.localStorage.getItem("view"));
    this.handleChangeTab(0);
  },
  methods: {
    handleChangeTab(tabActive) {
      switch (tabActive) {
        case 0:
          this.fnOpenFrame("information_nav_frm");
          break;
        case 1:
          this.fnOpenFrame("quotation_frm");
          break;
        case 2:
          this.fnOpenFrame("assets_frm");
          break;
        default:
          this.fnOpenFrame("account_frm");
      }
    },
    fnOpenFrame(name) {
      this.$ac.openFrame({
        name: name,
        url: `${name}.html`,
        rect: {
          x: 0,
          y: this.headerHeight,
          w: "auto",
          h: this.frameHeight
        },
        reload: true,
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

export default window.homeVue;
</script>

<style scoped lang="scss">





</style>