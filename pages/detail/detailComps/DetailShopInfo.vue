<template>
	 <view class="shop-info" v-if="Object.keys(shop).length !== 0">
	    <view class="shop-top">
	      <image :src="shop.logo" alt="" v-if="shop.logo" />
	      <text class="title">{{ shop.name }}</text>
	    </view>
	    <view class="shop-middle">
	      <view class="shop-middle-item shop-middle-left">
	        <view class="info-sells">
	          <view class="sells-count">
	            {{ shop.sells | sellCountFilter }}
	          </view>
	          <view class="sells-text">总销量</view>
	        </view>
	        <view class="info-goods">
	          <view class="goods-count">
	            {{ shop.goodsCount }}
	          </view>
	          <view class="goods-text">全部宝贝</view>
	        </view>
	      </view>
	      <view class="shop-middle-item shop-middle-right">
	        <table>
	          <tr :key="index" v-for="(item, index) in shop.score">
	            <td>{{ item.name }}</td>
	            <td :class="{ 'score-better': item.isBetter }" class="score">
	              {{ item.score }}
	            </td>
	            <td :class="{ 'better-more': item.isBetter }" class="better">
	              <text>{{ item.isBetter ? "高" : "低" }}</text>
	            </td>
	          </tr>
	        </table>
	      </view>
	    </view>
	    <view class="shop-bottom">
	      <view class="enter-shop">进店逛逛</view>
	    </view>
	  </view>
</template>

<script>
	export default {
	  name: "DetailShopInfo",
	  props: {
	    shop: {
	      type: Object,
	      default() {
	        return {};
	      }
	    }
	  },
	  filters: {
	    sellCountFilter(value) {
	      if (value < 10000) return value;
	      return (value / 10000).toFixed(1) + "万";
	    }
	  }
	};
</script>

<style lang="scss">
	.shop-info {
	  padding: 50rpx 16rpx;
	  border-bottom: 10rpx solid #f2f5f8;
	}
	
	.shop-top {
	  line-height: 90rpx;
	  display: flex;
	  align-items: center;
	}
	
	.shop-top image {
	  width: 90rpx;
	  height: 90rpx;
	  border: 1rpx solid rgba(0, 0, 0, 0.1);
	  border-radius: 50%;
	}
	
	.shop-top .title {
	  margin-left: 20rpx;
	  vertical-align: center;
	}
	
	.shop-middle {
	  display: flex;
	  align-items: center;
	  margin-top: 30rpx;
	}
	
	.shop-middle-item {
	  flex: 1;
	}
	
	.shop-middle-left {
	  display: flex;
	  justify-content: space-evenly;
	  text-align: center;
	  color: #333333;
	  border-right: 1rpx solid rgba(0, 0, 0, 0.1);
	}
	
	.sells-count,
	.goods-count {
	  font-size: 36rpx;
	}
	
	.sells-text,
	.goods-text {
	  font-size: 24rpx;
	  margin-top: 20rpx;
	}
	
	.shop-middle-right {
	  font-size: 26rpx;
	  color: #333333;
	}
	
	.shop-middle-right table {
	  width: 240rpx;
	  margin-left: 60rpx;
	}
	
	.shop-middle-right table td {
	  padding: 10rpx 0;
	}
	
	.shop-middle-right .score {
	  color: #5ea732;
	}
	
	.shop-middle-right .score-better {
	  color: #f13e3a;
	}
	
	.shop-middle-right .better text {
	  padding: 6rpx;
	  text-align: center;
	  color: #ffffff;
	  background-color: #5ea732;
	}
	
	.shop-middle-right .better-more text {
	  background-color: #f13e3a;
	}
	
	.shop-bottom {
	  margin-top: 20rpx;
	  text-align: center;
	}
	
	.enter-shop {
	  font-size: 28rpx;
	  line-height: 60rpx;
	  display: inline-block;
	  width: 300rpx;
	  height: 60rpx;
	  text-align: center;
	  border-radius: 10rpx;
	  background-color: #f2f5f8;
	}
</style>
