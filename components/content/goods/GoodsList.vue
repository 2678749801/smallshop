<template>
	  <view class="goods">
	    <goods-list-item 
	    v-for="(item,index) in goods" 
	    :goodsItem="item" 
	    :key="index"/>
	  </view>
</template>

<script>
	import GoodsListItem from './GoodsListItem.vue'
	
	export default {
	  components: { GoodsListItem },
	  name:'GoodsList',
	  props:{
	    goods:{
	      type:Array,
	      default(){
	        return[]
	      }
	    }
	  }
	}
</script>

<style lang="scss">
	.goods{
	  display: flex;
	  flex-wrap: wrap;
	  justify-content:space-around;
	}

</style>
