<template>
		<scroll-view scroll-y="true" class="tab-menu">
		<view class="menu-list">
		  <view class="menu-list-item"
		       :class="{active: index===currentIndex}"
		       v-for="(item, index) in categories"
		       :key="index"
		       @click="itemClick(index)">
		    {{item.title}}
		  </view>
		</view>
		</scroll-view>
</template>

<script>

	export default {
		name: "TabMenu",
    components: {
		
    },
    props: {
		  categories: Array
    },
    data() {
		  return {
		    currentIndex: 0
      }
    },
    methods: {
		  itemClick(index) {
        this.currentIndex = index
        this.$emit('selectItem', index)
      },
    
    },
	}
</script>

<style lang="scss">
  .tab-menu {
    background-color: #f6f6f6;
    height: calc(100% - 44px-49px);
    width: 100px;
    box-sizing: border-box;
    overflow: hidden;
		
		.menu-list-item {
		  height: 45px;
		  line-height: 45px;
		  text-align: center;
		  font-size: 14px;
		}
  }


 .active {
    font-weight: 700;
    color: #ff8198;
    background-color: #fff;
    border-left: 3px solid #ff8198;
  }
</style>
