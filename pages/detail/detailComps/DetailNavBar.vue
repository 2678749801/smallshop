<template>
		<view class="">
			<nav-bar>
				<view slot="center" class="title">
					<view
					v-for="(item,index) in titles"
					class="title-item"
					:key="index"
					:class="{active: index === currentIndex}"
					@click="titleClick(index)">
						{{item}}
					</view>
				</view>
			</nav-bar>

		</view>
</template>

<script>
	import NavBar from '../../../components/common/NavBar/NavBar.vue'
	export default{
		name:'DetailNavBar',
		  components:{
		    NavBar,
		  },
		  data() {
		    return {
		      titles:['商品','参数','评论','推荐'],
		      currentIndex:0
		    }
		  },
		  methods: {
		    titleClick(index){
		      this.currentIndex=index;
		      this.$emit('titleClick',index)
		    },
		  },
	}
</script>

<style lang="scss">
	.title{
	  display: flex;
	  font-size: 13px;
	}
	.title-item{
	  flex: 1;
	  
	}
	.active{
	  color:#ff8198;
	}
	.back img{
	  margin-top: 12px;
	}
</style>
