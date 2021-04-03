<template>
	<view class="detail">
		<detail-nav-bar/>
		<scroll-view scroll-y="true" >
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item v-for="(item,index) in topImages" :key="index">
					<image :src="item" alt="">
				</swiper-item>
			</swiper>
			<detail-base-info :goods="goods"></detail-base-info>
			<detail-shop-info :shop="shop"></detail-shop-info>
			<detail-images-info :images-info="imagesInfo"></detail-images-info>
		</scroll-view>
		<detail-bottom-bar @addToCart="addToCart" />
		<back-top @click.native="backClick" v-show="isShowBackTop" />
		  <view class="toast" v-show="show">
		    <view >{{message}}</view>
		  </view>
	</view>
</template>

<script>
	import DetailNavBar from './detailComps/DetailNavBar.vue'
	import DetailBaseInfo from './detailComps/DetailBaseInfo.vue'
	import DetailShopInfo from './detailComps/DetailShopInfo.vue'
	import DetailImagesInfo from './detailComps/DetailImageInfo.vue'
  import BackTop from '../../components/common/BackTop/BackTop.vue'
	import DetailBottomBar from './detailComps/DetailBottomBar.vue'
	import {
	  Goods,
	  Shop,
	  GoodsParams,
		
	} from '../../utils/detail.js'
	export default {
		components:{
			DetailNavBar,
			DetailBaseInfo,
			DetailShopInfo,
			DetailImagesInfo,
			DetailBottomBar,
			BackTop,
		},
		data() {
			return {
				iid: null,
				topImages: [],
				goods: {},
				shop: {},
				imagesInfo: {},
				paramInfo: {},
				commentInfo: {},
				themeTopYs: [], //是一个数组 不同的标题不同的位置
				currentIndex: 0,
				isShowBackTop: false,
				show:false,
				message:''
			}
		},
		onPageScroll(res){
				 this.isShowBackTop = res.scrollTop > 800;
		},
		onLoad(options) {
			this.iid=options.id
			this.getDetail(this.iid)
		},
		methods: {
			getDetail(iid){
				this.$myRequest({
					url: '/detail',
					data: {
							iid
					}
				}).then(res=>{
					const data = res.data.result;
					this.topImages = data.itemInfo.topImages;
					//获取商品信息
					this.goods = new Goods(
						data.itemInfo,
						data.columns,
						data.shopInfo.services
					);
					this.shop = new Shop(data.shopInfo);
				  this.imagesInfo = data.detailInfo;
					this.paramInfo = new GoodsParams(
						data.itemParams.info,
						data.itemParams.rule
					);
				})
			},
			backClick() {
				//父访问子 用子组件的功能
				uni.pageScrollTo({
					duration:0,
					scrollTop:0
				})
			},
			    addToCart() {
			      //获取商品信息添加到购物车
			      const product = {};
			      product.image = this.topImages[0];
			      product.title = this.goods.title;
			      product.desc = this.goods.desc;
			      product.price = this.goods.realPrice;
			      product.iid = this.iid;
			      //添加到购物车
			      this.$store.dispatch("addCart", product).then((res) => {
			        this.show=true;
			        this.message=res;
			        setTimeout(()=>{
			          this.show=false;
			          this.message=''
			        },1500)
			        // this.$toast.show(res, 2000);
							console.log('jiaru');
			      });
			    },
		}
	}
</script>

<style lang="scss">
.detail{
		swiper{
			width: 750rpx;
			height: 680rpx;
			image{
				height: 100%;
				width: 100%;	
		}
	}
}
.toast{
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  padding: 8px 10px;
  color: #fff;
  background-color: rgba(0,0,0,.5);
  z-index: 999;
}
</style>
