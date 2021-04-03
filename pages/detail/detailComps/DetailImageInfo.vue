<template>
	<view class="image-info" v-if="Object.keys(imagesInfo).length !== 0">
	    <view class="info-desc clear-fix">
	      <view class="start"></view>
	      <view class="desc">{{ imagesInfo.desc }}</view>
	      <view class="end"></view>
	    </view>
	    <view :key="index" v-for="(item, index) in imagesInfo.detailImage">
	      <view class="info-key">{{ item.key }}</view>
	      <view class="info-list">
	        <image
					  mode="aspectFit"
	          :key="imageIndex"
	          :src="image"
	          @load="imageLoad"
	          alt=""
	          v-for="(image, imageIndex) in item.list"
	        />
	      </view>
	    </view>
	  </view>
</template>

<script>
	export default {
	  name: "DetailImagesInfo",
	  data() {
	    return {
	      count: 0,
	      imagesLength: 0,
	    };
	  },
	  props: {
	    imagesInfo: {
	      type: Object,
	      default() {
	        return {};
	      },
	    },
	  },
	  methods: {
	    // imageLoad() {
	    //   if (++this.count === this.imagesLength) {
	    //     this.$emit("detailImageLoad");
	    //   }
	
	    // }
	    imageLoad() {
	      this.$emit("detailImageLoad");
	    },
	  },
	  watch: {
	    imagesInfo() {
	      this.imagesLength = this.imagesInfo.detailImage[0].list.length;
	    },
	  },
	};
</script>

<style lang="scss">
	.image-info {
	  padding: 20px 0;
	  border-bottom: 5px solid #f2f5f8;
	}
	
	.info-desc {
	  padding: 0 15px;
	}
	
	.info-desc .start,
	.info-desc .end {
	  position: relative;
	  width: 90px;
	  height: 1px;
	  background-color: #a3a3a5;
	}
	
	.info-desc .start {
	  float: left;
	}
	
	.info-desc .end {
	  float: right;
	}
	
	.info-desc .start::before,
	.info-desc .end::after {
	  position: absolute;
	  bottom: 0;
	  width: 5px;
	  height: 5px;
	  content: "";
	  background-color: #333333;
	}
	
	.info-desc .end::after {
	  right: 0;
	}
	
	.info-desc .desc {
	  font-size: 14px;
	  padding: 15px 0;
	}
	
	.info-key {
	  font-size: 15px;
	  margin: 10px 0 10px 15px;
	  color: #333333;
	}
	
	.info-list image {
	  width: 100%;
	}
</style>
