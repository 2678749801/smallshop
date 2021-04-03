<template>
    <view class="list">
      <view v-for="(item, index) in listData" :key="index" class="item">
        <view class="info">{{item.info}}</view>
      </view>
    </view>
</template>

<script>
	export default {
		name: "ListView",
    props: {
		  listData: {
		    type: Array,
        default: function () {
          return []
        }
      }
    }
	}
</script>

<style lang="scss">
  .list {
    background-color: #fff;
    font-size: 15px;
    color: #333;
		.item {
		  height: 44px;
		  line-height: 44px;
		  position: relative;
		}
		
		.info{
			margin-left: 40px;
			border-bottom: 1px solid rgba(100, 100, 100, .1);
			padding-left: 5px;
		}
  }

</style>
