 <template>
     <view class="home">
			 <tab-control :titles="titles" @tabClick="tabClick" ref="tabControl1"    class="tab-control" v-show="isTabFixed"></tab-control>
			<scroll-view scroll-y>
				<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
					<swiper-item v-for="(item,index) in banners" :key="index" >
						
						   <image :src="item.image" alt="" @click="swiperClick">
					</swiper-item>
				</swiper>
				<home-recommed-view :recommends="recommends" ></home-recommed-view>
				<image src="../../static/home/recommend_bg.jpg" mode="" style="width: 100%;"></image>
				<tab-control :titles="titles" @tabClick="tabClick" ref="tabControl2" class="getHeight"></tab-control>
				<!-- <goods-list :goods="goods[currentType].list"></goods-list> -->
				<mk-goods-list :goods="goods[currentType].list"></mk-goods-list>
			</scroll-view>
			<back-top @click.native="backClick" v-show="isShowBackTop" />
     </view>
 </template>  
 
 <script>
	 import HomeRecommedView from './childComps/HomeRecommendView.vue'
	 import TabControl from '../../components/content/tabcontrol/TabControl.vue'
	 import GoodsList from '../../components/content/goods/GoodsList.vue'
	 import MkGoodsList from '../../components/mk-goods-list/mk-goods-list.vue'
	 import BackTop from '../../components/common/BackTop/BackTop.vue'
 export default{
 components:{
		HomeRecommedView,
		TabControl,
		GoodsList,
		MkGoodsList,
		BackTop
 },
	 data(){
			 return {
					banners:[],
					recommends:[],
					titles: ["流行", "新款", "精选"],
					 currentType: "pop",
					 goods: {
						 pop: { page: 0, list: [] },
						 new: { page: 0, list: [] },
						 sell: { page: 0, list: [] },
					 },
					 isShowBackTop: false,
					 isTabFixed: false,
					 tabOffsetTop:0,
			 }
	 },
	 onLoad(){
		this.getMultidata(),
		    this.getHomeGoods("pop"); //一次请求三个数据
		    this.getHomeGoods("new");
		    this.getHomeGoods("sell");
				
	 },
	 onPageScroll(res){
		 this.isShowBackTop = res.scrollTop > 800;
		 this.isTabFixed = res.scrollTop > this.tabOffsetTop;
	 },
	 onReady() {
	 		 let that = this
	 		       uni.getSystemInfo({
	 		           success: function(res) { // res - 各种参数 
	 		             // console.log(res.windowHeight); // 屏幕的宽度
	 		             let info = uni.createSelectorQuery().select(".getHeight");// 获取某个元素
	 		             info.boundingClientRect(function(data) { //data - 各种参数
	 		             // console.log("获取的高度",data.top)  // 获取元素宽度
	 		             that.tabOffsetTop=data.top+data.height+data.height
	 		             }).exec()
	 		          }
	 		});
	 },
	 methods: {
		    swiperClick(){
					// console.log(plus)
				},
		async	getMultidata(){
				const res = await this.$myRequest({
					url:'/home/multidata',
					
				})
			 this.banners = res.data.data.banner.list;
			 this.recommends = res.data.data.recommend.list;
			},
			getHomeGoods(type) {
			      const page = this.goods[type].page + 1;
			      this.$myRequest({
							url: '/home/data',
							data: {
									type,
									page
							}
					}
						).then((res) => {
			        this.goods[type].list.push(...res.data.data.list); //将请求到的数据放进list里
			        this.goods[type].page += 1;
													
			      });
			    },
			tabClick(index) {
			      switch (index) {
			        case 0:
			          this.currentType = "pop"; //没有break会case穿透 执行到下一个break
			          break;
			        case 1:
			          this.currentType = "new";
			          break;
			        case 2:
			          this.currentType = "sell";
			      }
					this.$refs.tabControl1.currentIndex = index;
					this.$refs.tabControl2.currentIndex = index;
			    },
					backClick() {
						//父访问子 用子组件的功能
						uni.pageScrollTo({
							duration:0,
							scrollTop:0
						})
					},
			},
}
 </script>
 
 <style lang="scss">
.home{
	.tab-control {
	  position: fixed;
	  z-index: 92222;
	  background-color: #fff;
		width: 100%;
	}
	swiper{
		width: 750rpx;
		height: 380rpx;
		image{
			height: 100%;
			width: 100%;
		}
	}
}
 </style>