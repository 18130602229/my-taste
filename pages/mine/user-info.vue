<template>
	<view class="page">
		<nav-bar title="个人信息" bgColor="#F5f5f5"></nav-bar>
		<view class="cell_list" @click="onUnloadImg">
			<view class="cell_left txt">头像</view>
			<view class="cell_right">
				<image :src="headImg" mode="aspectFill"></image>
			</view>
		</view>
		<z-prompt :value="user.nickname" text="请输入昵称" @confirm="onNameChange" :options="popupOptions">
			<view class="cell_list">
				<view class="cell_left txt">昵称</view>
				<view class="cell_right arrow">{{ user.nickname }}</view>
			</view>
		</z-prompt>
		<view>
			<view class="cell_list">
				<view class="cell_left txt">性别</view>
				<picker class="cell_right arrow" :range="sexData" range-key="name" @change="onPickerChange" >
					<view class="select_info">
						<view class="value" v-if="pickerSex.name">{{ pickerSex.name }}</view>
						<view class="select" v-else>请选择</view>
					</view>
				</picker>
			</view>
		</view>
		<view>
			<view class="cell_list">
				<view class="cell_left txt">学历</view>
				<picker class="cell_right arrow" :range="degreeLevel" @change="onPickerDegreeChange" >
					<view class="select_info">
						<view class="value" v-if="user.degree">{{ user.degree }}</view>
						<view class="select" v-else>请选择</view>
					</view>
				</picker>
			</view>
		</view>
		<view>
			<view class="cell_list">
				<view class="cell_left txt">工作经验</view>
				<picker class="cell_right arrow" :range="jobExperienceData" @change="onPickerJobChange" >
					<view class="select_info">
						<view class="value" v-if="user.jobExperience">{{ user.jobExperience }}</view>
						<view class="select" v-else>请选择</view>
					</view>
				</picker>
			</view>
		</view>
		</z-prompt>
		<z-prompt :value="user.address" text="请输入现居地址" @confirm="onAddressChange" :options="popupOptions">
			<view class="cell_list">
				<view class="cell_left txt">地址</view>
				<view class="cell_right arrow">{{ user.address }}</view>
			</view>
		</z-prompt>
		<z-prompt :value="phone" text="请输入手机号" @confirm="onPhoneChange" :options="popupOptions">
			<view class="cell_list">
				<view class="cell_left txt">手机号</view>
				<view class="cell_right arrow">{{ phone }}</view>
			</view>
		</z-prompt>
		<!-- 按钮 -->
		<view class="form_but"><button class="active" @click="onSubmit">保存</button></view>
	</view>
</template>

<script>
	import zPrompt from '@/components/common/prompt';
	import {
		mapState,
		mapMutations
	} from 'vuex';
	export default {
		components: {
			zPrompt
		},
		data() {
			return {
				popupOptions: {
					placeholder: ''
				},
				headImg: 'https://lemon-test-use.oss-cn-beijing.aliyuncs.com/headImg/123',
				phone:'',
				user:{
					nickname: '',
					address:'',
					degree:'',
					jobExperience:'',
					origin:'',
					sex:''
				},
				jobExperienceData:['0 年','1年 ~ 2年','3年 ~ 4年','5年 ~ 10年','10+ 年'],
				degreeLevel:['小学','初中','高中','中专','大专','本科','硕士','博士'],
				sexData:[{
						name: '女',
						value: 0
					},
					{
						name: '男',
						value: 1
					}],
				pickerSex: {}
			};
		},
		computed: {
			...mapState(['userInfo'])
		},
		//第一次加载
		onLoad(e) {
			console.info("story userInfo:",this.userInfo);
			//根据token获取用户信息
			this.getUserInfo();
			this.phone = this.userInfo.info.phone;
			this.pickerSex = this.userInfo.info.sex<2?this.sexData[this.userInfo.info.sex]:{};
		},
		//页面显示
		onShow() {},
		//方法
		methods: {
			...mapMutations(['setUserInfo']),
			//修改昵称
			onNameChange(e) {
				this.user.nickname = e.value;
				e.close();
			},
			onPickerChange(e) {
				this.user.sex = e.detail.value;
				this.pickerSex = this.sexData[e.detail.value];
			},
			onAddressChange(e){
				console.info(e.value);
				if(this.user.address == ''){
					uni.showToast({
						title: '地址不能为空！',
						icon: 'none'
					});
					return;
				}
				this.user.address = e.value;
				e.close();
			},
			onPickerJobChange(e){
				console.info("job:",e.detail.value);
				this.user.jobExperience = this.jobExperienceData[e.detail.value];
			},
			onPickerDegreeChange(e){
				this.user.degree = this.degreeLevel[e.detail.value];
			},
			getUserInfo(){
				this.$http.get('user',{}).then(data => {
					this.user = data;
				});
			},
			//修改手机号
			onPhoneChange(e) {
				if (!this.$base.phoneRegular.test(e.value)) {
					uni.showToast({
						title: '请输入正确的手机号',
						icon: 'none'
					});
					return;
				}
				this.phone = e.value;
				e.close();
			},
			//修改头像
			onUnloadImg() {
				this.$http.urlImgUpload("user/head-img", {}).then(res => {
					console.info("upload headImg:",res)
					this.headImg = res;
				});
			},
			//提交
			onSubmit() {
				if (this.headImg == '') {
					uni.showToast({
						title: '请上传头像',
						icon: 'none'
					});
					return;
				}
				if (this.user.nickname == '') {
					uni.showToast({
						title: '请输入昵称',
						icon: 'none'
					});
					return;
				}
				// if(this.phone){
				// 	if (!this.$base.phoneRegular.test(this.phone)) {
				// 		uni.showToast({
				// 			title: '请输入正确的手机号',
				// 			icon: 'none'
				// 		});
				// 		return;
				// 	}
				// }
				this.$http
					.post('user', this.user)
					.then(res => {
						console.info("========xiu")
						// this.setUserInfo({
						// 	nickname: this.user.nickname,
						// 	headImg: this.headImg,
						// 	phone: this.phone || this.userInfo.phone
						// });
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
