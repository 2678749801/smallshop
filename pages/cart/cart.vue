<template>
  <view >
    <cart-list />
   <bottom-bar />
  </view>
</template>

<script>
import { mapGetters } from "vuex";
import CartList from "./childComps/CartList.vue";
import BottomBar from "./childComps/BottomBar.vue";
export default {
  components: {  CartList, BottomBar },
  name: "Cart",
  computed: {
    //将getters里的东西转换成计算属性
    ...mapGetters(["cartLength"]),
  },
};
</script>

<style lang="scss">
#cart {
  
}
.nav-bar {
  background-color: #ff8198;
  color: #fff;
}
</style>