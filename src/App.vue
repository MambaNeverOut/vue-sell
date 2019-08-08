<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab-wrapper">
      <tab :tabs="tabs"></tab>
    </div>
  </div>
</template>

<script>
import VHeader from "components/v-header/v-header";
import { getSeller } from "api";
import Tab from "components/tab/tab";
import Seller from "components/seller/seller";
import Goods from "components/goods/goods";
import Ratings from "components/ratings/ratings";

export default {
  name: "app",
  data() {
    return {
      seller: {}
    };
  },
  computed: {
    tabs() {
      return [
        {
          label: "商品",
          component: Goods,
          data: {
            seller: this.seller
          }
        },
        {
          label: "评论",
          component: Ratings,
          data: {
            seller: this.seller
          }
        },
        {
          label: "商家",
          component: Seller,
          data: {
            seller: this.seller
          }
        }
      ];
    }
  },
  components: {
    VHeader,
    Tab
  },
  created() {
    this._getSeller();
  },
  methods: {
    _getSeller() {
      getSeller().then(seller => {
        this.seller = seller;
      });
    }
  }
};
</script>
<style lang="stylus">
#app {
  .tab-wrapper {
    position: fixed;
    top: 136px;
    left: 0;
    right: 0;
    bottom: 0;
  }
}
</style>
