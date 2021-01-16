<template>
	<view>
		<nav-bar title="学习列表" bgColor="#F5f5f5"></nav-bar>
		<view>
			<uni-section title="进行中学习" type="line"></uni-section>
			<view class="example-body">
				<view class="example-box">
					<uni-card title="解答问题" :isFull="true" isShadow='true' note="已同意" extra="2020-01-12" @click="clickCard"><text class="content-box-text">通栏卡片，左右上下没有间距，用户可自定没有间距，用户可自定义没有间距，用户可自定义义卡片距离等信息</text></uni-card>
				</view>
			</view>
		</view>
		<view>
			<uni-section title="完成学习" type="line"></uni-section>
			<view class="example-body">
				<view class="example-box">
					<uni-card title="解答问题" :isFull="true" isShadow='true' note="已同意" extra="2020-01-12" @click="clickCard"><text class="content-box-text">通栏卡片，左右上下没有间距，用户可自定没有间距，用户可自定义没有间距，用户可自定义义卡片距离等信息</text></uni-card>
				</view>
				<view class="example-box">
					<uni-card title="解答问题" :isFull="true" isShadow='true' note="已同意" extra="2020-01-12" @click="clickCard"><text class="content-box-text">通栏卡片，左右上下没有间距，用户可自定没有间距，用户可自定义没有间距，用户可自定义义卡片距离等信息</text></uni-card>
				</view>
				<view class="example-box">
					<uni-card title="解答问题" :isFull="true" isShadow='true' note="已同意" extra="2020-01-12" @click="clickCard"><text class="content-box-text">通栏卡片，左右上下没有间距，用户可自定没有间距，用户可自定义没有间距，用户可自定义义卡片距离等信息</text></uni-card>
				</view>
			</view>
		</view>
		<view>
			<uni-section title="未完成学习" type="line"></uni-section>
			<view class="example-body">
				<view class="example-box">
					<uni-card title="解答问题" :isFull="true" isShadow='true' note="已同意" extra="2020-01-12" @click="clickCard"><text class="content-box-text">通栏卡片，左右上下没有间距，用户可自定没有间距，用户可自定义没有间距，用户可自定义义卡片距离等信息</text></uni-card>
				</view>
			</view>
		</view>
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
			}
		},
		methods: {
			clickCard() {
				uni.showToast({
					title: '点击卡片',
					icon: 'none'
				})
			}
		}
	}
</script>

<style>
	.example-body {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
		padding: 0;
		font-size: 14px;
		background-color: #ffffff;
	}
	.example-box {
		margin: 12px 0;
	}
	.content-box-text {
		font-size: 12px;
		line-height: 22px;
	}
</style>
