<template>
	<view>
		<nav-bar backState="2000" title="我的消息"></nav-bar>
		<!-- 公共组件-每个页面必须引入 -->
		<public-module></public-module>
		<view class="notice-type">
			<view>通知</view>
			<view>系统</view>
			<view>消息</view>
		</view>
		
		<z-navigation></z-navigation>
	</view>
</template>

<script>
import zNavigation from '@/components/module/navigation.vue';
export default {
	components: {
		zNavigation
	},
	data() {
		return {};
	},
	//第一次加载
	onLoad(e) {
		// 隐藏原生的tabbar
		uni.hideTabBar();
	},
	//页面显示
	onShow() {
		// 隐藏原生的tabbar
		uni.hideTabBar();
	},
	//方法
	methods: {
	},
	//页面隐藏
	onHide() {},
	//页面卸载
	onUnload() {},
	//页面下来刷新
	onPullDownRefresh() {},
	//页面上拉触底
	onReachBottom() {},
	//用户点击分享
	onShareAppMessage(e) {
		return this.wxShare();
	}
};
</script>
<style lang="scss" scoped>
@import '@/style/mixin.scss';
.notice-type{
	margin-top: 10rpx;
	display: flex;
	view{
		color: #f00;
		width: 33%;
		border: 1rpx;
		text-align: center;
		border: 1px solid;
	}
}
</style>
