<template>
	<view class="page">
		<nav-bar title="学习" bgColor="#F5f5f5"></nav-bar>
		<view class="input_form_box">
			<view class="input_box btm_line">
				<view class="name required">问题</view>
				<view class="input_info"><input type="text" placeholder="请输入" /></view>
			</view>
			<view class="input_box">
				<view class="name required">描述</view>
				<view class="textarea_info"><textarea placeholder="请输入问题背景和自己了解情况"></textarea></view>
			</view>
			<view class="input_box btm_line">
				<view class="name required">难度系数</view>
				<picker :range="difficultyLevel" @change="onPickerChange">
					<view class="select_info">
						<view class="value" v-if="difficultyFactor">{{ difficultyFactor }}</view>
						<view class="select" v-else>请选择</view>
					</view>
				</picker>
			</view>
			<view class="input_box btm_line">
				<view class="name required">类型</view>
				<view class="input_info"><input type="text" placeholder="请输入问题类型" /></view>
			</view>
			<view class="input_box">
				<view class="name required">见面地址</view>
				<view class="select_info" @click="popupShow = true">
					<text class="value" v-if="addressList4.length == 3">{{ addressList4[0].name }}{{ addressList4[1].name }}{{ addressList4[2].name }}</text>
					<text class="value" v-else-if="addressList4.length == 2">{{ addressList4[0].name }}{{ addressList4[1].name }}</text>
					<text class="value" v-else-if="addressList4.length == 1">{{ addressList4[0].name }}</text>
					<text class="select" v-else="">请选择地址</text>
				</view>
			</view>
			
		</view>
		<!-- 按钮 -->
		<view class="form_but"><button class="active" @click="onSubmit">保存</button></view>
		<view class="form_but"><button class="active" @click="onSubmit">发布</button></view>
		<address-popup v-model="popupShow" :length="3" :force="false"  @change="addressChange4"></address-popup>
		
	</view>
</template>

<script>
	import addressPopup from '@/components/common/address-popup';
	import zAddress from '@/components/common/address';
	import zPrompt from '@/components/common/prompt';
	export default {
		components: {
			addressPopup,
			zAddress,
			zPrompt
		},
		data() {
			return {
				popupOptions: {
					placeholder: ''
				},
				study:{
					title:'',
					described:'',
					difficultyFactor:'',
					type:'',
					time:'',
					address:''
				},
				difficultyFactor:'',// 显示难度系数 文字描述
				difficultyLevel:["低","中","高"],
				popupShow: false,
				addressList4:[]
			};
		},
		//页面显示
		onShow() {},
		//方法
		methods: {
			//问题难度系数选择
			onPickerChange(e) {
				this.study.difficultyFactor = e.detail.value;
				this.difficultyFactor = this.difficultyLevel[e.detail.value];
			},
			// 选择见面地址
			addressChange4(e) {
				console.log(e);
				this.addressList4 = e;
			},
			//提交
			onSubmit() {
				if (this.avatar == '') {
					uni.showToast({
						title: '请上传头像',
						icon: 'none'
					});
					return;
				}
				if (this.nickname == '') {
					uni.showToast({
						title: '请输入昵称',
						icon: 'none'
					});
					return;
				}
				let httpData = {
					nickname: this.nickname,
					avatar: this.avatar
				};
				if(this.phone){
					if (!this.$base.phoneRegular.test(this.phone)) {
						uni.showToast({
							title: '请输入正确的手机号',
							icon: 'none'
						});
						return;
					}
					if(this.phone != this.userInfo.phone){
						httpData.phone = this.phone;
					}
				}
				this.$http
					.post('api/common/v1/edit_user_info', httpData)
					.then(res => {
						uni.showToast({
							title: '修改成功！'
						});
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

<style lang="scss" scoped>
	@import '@/style/mixin.scss';
	.cell_list {
		padding: 30rpx 30rpx;
		margin: 20rpx 30rpx 0 30rpx;
		border-radius: 8rpx;
	}

	.cell_right image {
		width: 140rpx;
		height: 140rpx;
		border-radius: 50%;
	}
</style>
