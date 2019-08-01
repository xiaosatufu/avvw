<template>
  <div>
    <Tabs
      v-model="active"
      line-width="0"
      title-inactive-color="#161616"
      title-active-color="#F58220"
      :border="false"
      id="informationTabs"
    >
      <Tab title="精选"></Tab>
      <Tab title="快讯"></Tab>
    </Tabs>
  </div>
</template>

<script>
import { Tab, Tabs } from "vant";
import apicloud from "@/libs/apicloud";

window.information_nav_frmVue = {
  name: "information_nav_frm",
  components: { Tab, Tabs },
  data() {
    return {
      active: 0,
      view:{}
    };
  },
  mounted() {

      
    // alert('nav' + window.localStorage.getItem('view'))

    this.view = JSON.parse(window.localStorage.getItem('view'))

    // alert('view' + this.view.headerHeight)
    // alert('view' + this.view.frameHeight)


    // alert(2);

    // alert('nav_frm',JSON.parse(window.localStorage.getItem('view')))

    // let headerHeight = apicloud.dom("#header").offsetHeight;

    // alert('111'+ headerHeight);
    // let footerHeight = apicloud.dom("#tabbar").offsetHeight;

    let informationTabsHeight = apicloud.dom("#informationTabs").offsetHeight;

    let frameHeight =this.view.frameHeight*1 - informationTabsHeight*1;


    this.$ac.openFrameGroup(
      {
        name: "information_group",
        scrollEnabled: true,
        rect: {
          x: 0,
          y: this.view.headerHeight + informationTabsHeight,
          w: "auto",
          h: frameHeight
        },
        index: 0,
        useWKWebView: true, // Be careful here
        historyGestureEnabled: true,
        frames: [
          {
            name: "information_selected_frm",
            url: "information_selected_frm.html",
            bounces: true
          },
          {
            name: "information_newsflash_frm",
            url: "information_newsflash_frm.html",
            bounces: true
          }
        ]
      },
      (ret, err) => {
        // You must use arrow function that can been used 'THIS'
        this.tabActive = ret.index;
      }
    );
  },
  methods: {}
};

export default window.information_nav_frmVue;
</script>

<style lang="scss" scoped>
</style>