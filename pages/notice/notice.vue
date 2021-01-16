<template>
	<view>
		<nav-bar backState="2000" title="我的消息"></nav-bar>
		<view class="end-title">
		　　<view @tap="change(0)" :class="{btna:btnnum == 0}">通知</view>
		  　<view @tap="change(1)" :class="{btna:btnnum == 1}">系统</view>
		　　<view @tap="change(2)" :class="{btna:btnnum == 2}">消息</view>
		</view>
		<view class="end-cont" :class="{dis:btnnum == 0}">
		 　　0信息
		</view>
		<view class="end-cont" :class="{dis:btnnum == 1}">
		 　　1信息
		</view>
		<view class="end-cont" :class="{dis:btnnum == 2}">
		  　2信息
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
			      btnnum: 0,
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
		   change(e) {
		      this.btnnum = e
		      console.log(this.btnnum)
		  }
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

    /* 将三个内容view的display设置为none(隐藏) */
    .end-title{
        display: flex;
    }
    .end-title view{
        flex-grow: 1;
        text-align: center;
    }
    .end-cont{
        display: none;
        background: #C8C7CC;
    }
    .btna{
        color: #FFFFFF;
        background: #00A0FF;
    }
    .dis{
        display: block;
    }    
</style>
