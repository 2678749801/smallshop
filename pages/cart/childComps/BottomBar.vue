<template>
  <view class="bottom-menu">
    <CheckButton class="select-all" :isChecked="isSelectAll" @click.native="checkClick"></CheckButton>
    <text>全选</text>
    <text class="total-price">合计: ¥{{totalPrice}}</text>
    <text class="buy-product">去计算({{$store.getters.cartCount}})</text>
  </view>
</template>

<script>
import { mapGetters } from 'vuex';
  import CheckButton from './CheckButton'

	export default {
		name: "BottomBar",
    components: {
		  CheckButton
    },
    computed: {
      ...mapGetters(['cartList']),
		  totalPrice() {
        const cartList = this.$store.getters.cartList;
        return cartList.filter(item => {
          return item.checked
        }).reduce((preValue, item) => {
          return preValue + item.count * item.price
        }, 0).toFixed(2)
      },
      checkLength(){
        return this.cartList.filter(item=>item.checked).length
      },
      isSelectAll: function () {
        if(this.cartList.length === 0) return false
        // return !this.cartList.find(item => item.checked )
        for(let item of this.cartList){
          if (!item.checked) {
            return false
          }
        }
        return true
      }
    },
    methods: {
     checkClick(){
       if (this.isSelectAll) {
         this.cartList.forEach(item=>item.checked=false)
       }else{
         this.cartList.forEach(item=>item.checked=true)
       }
     }
    }
	}
</script>

<style  scoped lang="scss">
  .bottom-menu {
    width: 100%;
    height: 88rpx;
    background-color: #eee;
    position: fixed;
    bottom: 0rpx;
    left: 0;
    box-shadow: 0 -2px 3px rgba(0, 0, 0, .2);
    font-size: 28rpx;
    color: #888;
    line-height: 88rpx;
    padding-left: 70rpx;
    box-sizing: border-box;
		.select-all {
		  position: absolute;
		  line-height: 0;
		  left: 24rpx;
		  top: 26rpx;
		}
		.total-price {
		  margin-left: 15px;
		  font-size: 16px;
		  color: #666;
		}
		.buy-product {
		  background-color: orangered;
		  color: #fff;
		  width: 200rpx;
		  height: 88rpx;
		  text-align: center;
		  line-height: 88rpx;
		  float: right;
		}
  }



</style>
