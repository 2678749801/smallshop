<template>
      <view class="check-button" :class="{check: isChecked}">
      <image src="../../../static/cart/tick.svg" mode="scaleToFill" alt="">
    </view>
</template>

<script>
	export default {
    name: "CheckButton",
    props:{
      isChecked:{
        type:Boolean,
        default:false
      }
    },
   methods:{
		 
	 }
	}
</script>

<style lang="scss">
  .check-button{
    
    border-radius: 50%;
    border: 2px solid #aaa;
		image{
			width: 25rpx;
			height: 25rpx;
		}

  }
	.check{
	  background-color:red;
	  border-color: red;
	}

</style>
