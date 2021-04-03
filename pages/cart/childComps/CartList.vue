<template>
    <view class="cart-list">

    <cart-list-item v-for="item in cartList" :key="item.iid" :item-info="item"></cart-list-item>
  

  </view>
</template>

<script>

  import CartListItem from './CartListItem'
  import { mapGetters } from 'vuex'
	export default {
		name: "CartList",
    components: {
		 CartListItem
    },
    computed:{
      ...mapGetters(['cartList'])
    }
	}
</script>

<style >

</style>
