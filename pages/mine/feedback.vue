<template>
	<view>
		<nav-bar title="意见反馈" bgColor="#F5f5f5"></nav-bar>
		<view class="main-page"> 
			<view>
				<view><image src="../../static/share/icon_copy.png"></image><text>反馈内容</text></view>
				<view class="textarea_info"><textarea v-model="feedback.content" placeholder="请输入问题背景和自己了解情况"></textarea></view>
			</view>
			<view>
				<view><image src="../../static/demo/ic_video_phone.png"></image><text>联系方式</text></view>
				<input class="uni-input" name="nickname" v-model="feedback.contact" placeholder="请输入联系方式" />
			</view>
			<button type="primary" @click="onSubmit">提交</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				feedback:{
					content:'',
					contact:''
				}
			};
		},
		//页面显示
		onShow() {},
		//方法
		methods: {
			onSubmit(){
				this.$http
					.post('feedback', this.feedback)
					.then(res => {
						console.info("result:",res)
						uni.showToast({
							title: '修改成功！'
						});
						setTimeout(() => {
							uni.navigateBack();
						}, 1000);
					});
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

<style>
	.main-page{
		padding: 20px 15px;
	}
	image{
		width: 20px;
		height: 20px;
	}
	input{
		border: #808080 2rpx solid;
		height: 56rpx;
	}
	button{
		margin-top: 20px;
	}
</style>
