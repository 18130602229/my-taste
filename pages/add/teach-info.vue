<template>
	<view>
		<view>
			<uni-section title="进行中教学" type="line"></uni-section>
			<view class="example-body">
				<view class="example-box">
					<uni-card title="解答教学" :isFull="true" isShadow='true' note="已同意" extra="2020-01-16" @click="clickCard"><text class="content-box-text">通栏卡片，左右上下没有间距，用户可自定义卡片距离等信息有间距，用户可自定义卡片距有间距，用户可自定义卡片距有间距，用户可自定义卡片距有间距，用户可自定义卡片距</text></uni-card>
				</view>
			</view>
		</view>
		<view>
			<uni-section title="完成教学" type="line"></uni-section>
			<view class="example-body">
				<view class="example-box">
					<uni-card title="解答教学" :isFull="true" isShadow='true' note="已同意" extra="2020-01-16" @click="clickCard"><text class="content-box-text">通栏卡片，左右上下没有间距，用户可自定义卡片距离等信息有间距，用户可自定义卡片距有间距，用户可自定义卡片距有间距，用户可自定义卡片距有间距，用户可自定义卡片距</text></uni-card>
				</view>
				<view class="example-box">
					<uni-card title="解答教学" :isFull="true" isShadow='true' note="已同意" extra="2020-01-16" @click="clickCard"><text class="content-box-text">通栏卡片，左右上下没有间距，用户可自定义卡片距离等信息有间距，用户可自定义卡片距有间距，用户可自定义卡片距有间距，用户可自定义卡片距有间距，用户可自定义卡片距</text></uni-card>
				</view>
				<view class="example-box">
					<uni-card title="解答教学" :isFull="true" isShadow='true' note="已同意" extra="2020-01-16" @click="clickCard"><text class="content-box-text">通栏卡片，左右上下没有间距，用户可自定义卡片距离等信息有间距，用户可自定义卡片距有间距，用户可自定义卡片距有间距，用户可自定义卡片距有间距，用户可自定义卡片距</text></uni-card>
				</view>
			</view>
		</view>
		<view>
			<uni-section title="其它教学教学" type="line"></uni-section>
			<view class="example-body">
				<view class="example-box">
					<uni-card title="解答教学" :isFull="true" isShadow='true' note="已同意" extra="2020-01-16" @click="clickCard"><text class="content-box-text">通栏卡片，左右上下没有间距，用户可自定义卡片距离等信息有间距，用户可自定义卡片距有间距，用户可自定义卡片距有间距，用户可自定义卡片距有间距，用户可自定义卡片距</text></uni-card>
				</view>
			</view>
		</view>
	</view>

	
</template>

<script>
	import uniSection from '@/components/uni-section/uni-section';
		import uniCard from '@/components/uni-card/uni-card';
	export default {
		components: {
			uniSection,
			uniCard
		},
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
