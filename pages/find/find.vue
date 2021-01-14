<template>
	<view>
		<!-- <nav-bar title="轮播图"></nav-bar> -->
		<!-- 公共组件-每个页面必须引入 -->
		<public-module></public-module>
		<!-- banner -->
		<view class="banner_swiper_box">
			<swiper class="banner_swiper" indicator-dots :autoplay="true" :interval="3000" circular previous-margin="30px" next-margin="30px" :duration="1000" @change="onSwiperChange">
				<swiper-item v-for="(item, index) of bannerList" :key="index">
					<view class="banner_img" :class="{ active: swiperIndex == index }">
						<image src="../../static/demo/1.jpg" mode="aspectFill" @click="onBanner(item)"></image>
					</view>
				</swiper-item>
			</swiper>
		</view>
		
		<view class="little-nva">
			<view>推荐</view>
			<view>教学</view>
			<view>最新</view>
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
		return {
			swiperIndex: 0,
			bannerList: [1, 1, 1, 1]
		};
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
		// 轮播图变化
		onSwiperChange(e) {
			this.swiperIndex = e.detail.current;
		},
		// 轮播图点击
		onBanner(item) {
			this.$http.post("user/login", {
				account: 'root',
				password: 'root'
			},{
				isPrompt: true,//（默认 true 说明：本接口抛出的错误是否提示）
				load: true,//（默认 true 说明：本接口是否提示加载动画）
				header: { //默认 无 说明：请求头
					'Content-Type': 'application/x-www-form-urlencoded'
				},
				isFactory: true //（默认 true 说明：本接口是否调用公共的数据处理方法，设置false后isPrompt参数将失去作用）
			}).then(res => {
				console.log("接口获取成功! 数据 =>",res);
			});
		},
		onPageJump(url) {
			uni.navigateTo({
				url: url
			});
		}
	},
	//用户点击分享
	onShareAppMessage(e) {
		return this.wxShare();
	}
};
</script>
<style lang="scss" scoped>
@import '@/style/mixin.scss';
.little-nva{
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
.banner_swiper_box {
	padding-top: 15upx;
	background-color: #fff;
	.banner_swiper {
		height: 315upx;

		swiper-item {
			box-sizing: border-box;
			display: flex;
			align-items: center;
			.banner_img {
				width: 100%;
				height: 100%;
				transform: scale(0.9);
				transition: all 0.4s;
				&.active {
					transform: scale(1);
				}
				image {
					width: 100%;
					height: 100%;
					box-shadow: 0upx 20upx 30upx 0upx rgba(0, 0, 0, 0.1);
					border-radius: 20upx;
				}
			}
		}
	}
}
</style>
