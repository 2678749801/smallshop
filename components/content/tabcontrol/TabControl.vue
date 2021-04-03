<template>
		<view class="tabcontrol">
			<view  v-for="(item,index) in titles" 
	    class="tabcontrol-item"
	    :key="index"
	    :class="{active:index===currentIndex}"
	    @click="itemClick(index)"
			>
				<text>{{item}}</text>
			</view>
		</view>
</template>

<script>
	export default {
	  name:"TabControl",
	  props:{
	    titles:{
	      type:Array,
	      default(){
	        return[]
	      }
	    }
	  },
	  data() {
	    return {
	      currentIndex:0
	    }
	  },
	  methods: {
	    itemClick(index){
	      this.currentIndex=index;
	      this.$emit('tabClick',index)
	    }
	  },
	}
</script>

<style lang="scss">
	.tabcontrol{
	  display: flex;
	  text-align: center;
	  font-size: 15px;
		.tabcontrol-item{
		  flex: 1;
		  height: 40px;
		  line-height: 40px;
				text{
			  padding: 5px;
			}
		}
	}


	.active{
	  color:#ff8198;
	  
	}
	.active text{
	border-bottom: 3px solid #ff8198;
	}
</style>
