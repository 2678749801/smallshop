<template>
  <view class="shop-item">
  <view class="item-selector">
      <CheckButton @click.native="checkClick" :is-checked="itemInfo.checked" ></CheckButton>
    </view>
    <view class="item-image">
      <image :src="itemInfo.image" alt="商品图片">
    </view>
    <view class="item-info">
      <view class="item-title">{{itemInfo.title}}</view>
      <view class="item-desc">商品描述: {{itemInfo.desc}}</view>
      <view class="info-bottom">
        <view class="item-price left">¥{{itemInfo.price}}</view>
        <view class="item-count-right">x{{itemInfo.count}}</view>
      </view>
    </view>
  </view>
</template>

<script>
  import CheckButton from './CheckButton'

  export default {
    name: "CartListItem",
    props: {
      itemInfo: Object
    },
    components: {
      CheckButton
    },
    methods: {
      checkClick(){
        this.itemInfo.checked = !this.itemInfo.checked
      }
    }
  }
</script>

<style lang="scss">
	.shop-item{
		width: 100%;
		font-size: 0;
		display: flex;
		  padding: 10rpx;
		  border-bottom: 1px solid #ccc;
			.item-selector {
			  width: 14%;
			  display: flex;
			  justify-content: center;
			  align-items: center;
			}
		.item-image{
			padding: 5px;
			image{
				width: 160rpx;
				height: 200rpx;
				display: block;
				border-radius: 10rpx;
			}
		}
		.item-info{
			font-size: 34rpx;
			color: #333;
			padding: 10rpx 20rpx;
			position: relative;
			overflow: hidden;
			.item-title,
			.item-desc {
			  overflow: hidden;
			  white-space: nowrap;
			  text-overflow: ellipsis;
			}
			.item-desc {
			  font-size: 28rpx;
			  color: #666;
			  margin-top: 30rpx;
			}
			.info-bottom {
			  margin-top: 20rpx;
			  position: absolute;
			  bottom: 20rpx;
			  left: 20rpx;
			  right: 20rpx;
				float: right;
				.item-price {
				  color: orangered;
				}
			}
		}
	}


 
</style>
