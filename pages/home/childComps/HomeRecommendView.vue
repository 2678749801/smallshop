<template>
		<view class="recommends">
			<view v-for="(item,index) in recommends"  class="recommend-item" :key="index">
				<image :src="item.image" mode=""></image>
				<view>{{item.title}}</view>
			</view>
		</view>
</template>

<script>
	export default{
		props: {
		    recommends: {
		      type: Array,
		      default() {
		        return [];
		      },
		    },
		  },
	}
</script>

<style lang="scss">
	.recommends {
	  display: flex;
	  text-align: center;
	  width: 100%;
	  font-size: 12px;
	  padding: 15px 0 30px;
	  border-bottom: 8px solid#eee;
		.recommend-item {
		  flex: 1;
		}
		.recommend-item image {
		  width: 65px;
		  height: 65px;
		}
	}


	
</style>
