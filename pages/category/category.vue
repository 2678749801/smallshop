<template>
	<view class="category">
		    <view class="content">
		      <tab-menu :categories="categories"></tab-menu>
		    </view>	  
	</view>
</template>

<script>
	import TabMenu from './categoryComps/TabMenu.vue'
	export default {
		components:{
			TabMenu,
		},
		data() {
			return {
				categories: [],
				 categoryData: {},
				currentIndex: -1,
			}
		},
		onLoad() {
			this.getCategory()
		},
		methods: {		
			 getCategory(){
				 this.$myRequest({
					 url: '/category'
				 }).then(res=>{
					  this.categories = res.data.data.category.list					
				 })
			 },			 
		},	
	}
</script>

<style>

</style>
