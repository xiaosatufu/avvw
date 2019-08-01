<template>
  <div>
    <Tabbar
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
    </Tabbar>
  </div>
</template>

<script>
import { Tabbar, TabbarItem } from "vant"; // Dynamic import is a good idea to keep ur page slim and fast
import apicloud from "@/libs/apicloud";
export default {
  name: "footer",
  components: { Tabbar, TabbarItem },
  data() {
    return {
      tabActive: 0,
      icon: [
        {
          normal: require("@/images/tabBar/new_icn@3x.png"),
          active: require("@/images/tabBar/newOn_icn@3x.png")
        },
        {
          normal: require("@/images/tabBar/price_icn@3x.png"),
          active: require("@/images/tabBar/priceOn_icn@3x.png")
        },
        {
          normal: require("@/images/tabBar/assets_icn@3x.png"),
          active: require("@/images/tabBar/assetsOn_icn@3x.png")
        },
        {
          normal: require("@/images/tabBar/user_icn@3x.png"),
          active: require("@/images/tabBar/UserOn_icn@3x.png")
        }
      ]
    };
  },
  mounted() {
    apicloud.fixTabBar(apicloud.dom("#tabbar")); // Fix the APP header bug
  },
  methods: {
    changeTab() {
      this.$emit("changeTab", this.tabActive);
    }
  }
};
</script>

<style lang="scss" scoped>
#tabbar {
  position: fixed;
} 
</style>