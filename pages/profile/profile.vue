<template>
  <view class="profile">
<!--    <nav-bar class="nav-bar"><view slot="center">个人中心</view></nav-bar> -->
    <!--1.单独封装一个组件: 利用slot知识点-->
    <!-- <UserInfo></UserInfo> -->

    <!--2.没有单独封装: 不同的地方太多, 需要传过多的参数-->
    <section class="account">
      <view class="account-item">
        <view class="number"><text class="balance">0.00</text>元</view>
        <view class="account-info">我的余额</view>
      </view>
      <view class="account-item">
        <view class="number"><text class="balance">0</text>个</view>
        <view class="account-info">我的优惠</view>
      </view>
      <view class="account-item">
        <view class="number"><text class="balance">0</text>分</view>
        <view class="account-info">我的积分</view>
      </view>
    </section>

    <!--3.封装成一个整体-->
   <list-view :list-data="orderList" class="order-list"></list-view>
    <list-view :list-data="serviceList" class="service-list"></list-view>
  </view>
</template>

<script>
import ListView from "./ListView";
export default {
  name: "Profile",
  components: {
    ListView,
  },
  data() {
    return {
      orderList: [
        { icon: "#order", iconColor: "#ff8198", info: "我的消息" },
        { icon: "#point", iconColor: "#fc7b53", info: "积分商城" },
        { icon: "#vip", iconColor: "#ffc636", info: "会员卡" },
      ],
      serviceList: [
        { icon: "#service", iconColor: "#ff8198", info: "我的购物车" },
        { icon: "#download", iconColor: "#ff8198", info: "下载购物APP" },
      ],
    };
  },
};
</script>

<style lang="scss">
.profile {
  background-color: #f2f2f2;
	.account {
	  display: flex;
		.account-item {
		  width: 100%;
		  background-color: #fff;
		  margin-right: 1px;
		  text-align: center;
			color: #666;
			font-size: 13px;
			padding: 18px;
			.account-info {
			  margin-top: 6px;
			}
			.number{
				.balance {
				  font-size: 24px;
				  font-weight: 700;
				  color: #ff5f3e;
				}
			}
		}
	}
}
</style>
