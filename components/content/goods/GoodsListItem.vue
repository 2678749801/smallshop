<template>
		<view class="goods-item" >
			<image :src="goodsItem.show.img" mode=""></image>
			<view class="">
				<view class="goods-info">
					<text>{{goodsItem.title}}</text>
					<text class="price">{{goodsItem.price}}</text>
					<text class="collect">{{goodsItem.cfav}}</text>
				</view>
			</view>
		</view>
</template>

<script>
	export default {
	  name:"GoodsListItem",
	  props:{
	    goodsItem:{
	      type:Object,
	      default(){
	        return[]
	      }
	    }
	  },
	  methods: {
	    // imageLoad(){//load事件 加载完成调用 
	    //   this.$bus.$emit('itemImageLoad')
	    // },
	    // itemClick(){
	    //   this.$router.push('/detail/' + this.goodsItem.iid)
	    // }
	  },
	}
</script>

<style lang="scss">
	.goods-item{
	  padding-bottom: 40px;
	  position: relative;
	  width: 48%;
		image{
		  width: 100%;
		  border-radius: 5px;
		}
		.goods-info{
		  font-size: 12px;
		  position: absolute;
		  bottom: 5px;
		  left: 0;
		  right: 0;
		  overflow: hidden;
		  text-align: center;
			text{
				overflow: hidden;
				text-overflow: ellipsis;
				white-space: nowrap;
					 
				margin-bottom: 3px;}
				.price{
				  color:var(--color-high-text);
				  margin-right: 20px;
				}
				.collect{
				  position: relative;
				}
				.collect::before{
				  content: '';
				  position: absolute;
				  left: -15px;
				  top: -1px;
				  width: 14px;
				  height: 14px;
				  // background: url("~assets/img/common/collect.png") 0 0/14px 14px;
				}
			
			
		}

		
	}

	

</style>
