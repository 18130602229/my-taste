<template>
	<view class="page">
		<nav-bar title="教授" bgColor="#F5f5f5"></nav-bar>
		<view class="input_form_box">
			<view style="padding: 20rpx 30rpx;border-bottom: 2rpx solid #ccc;">
				<view class="user_info">
					<image src="../../static/demo/1.jpg"></image>
					<view>
						<view>张三</view>
						<view style="font-size: 28rpx;">深圳南山区</view>
					</view>
					<view class="question_time" style="font-size: 28rpx; ">2020/01/16</view>
				</view>
				<view style="display: flex;" @click="moreInfo()">
					<view style="font-size: 32rpx; padding-left: 40rpx;margin-top: 40rpx;">现在失业，没有方向，该怎么办？</view>
					<radio value="r1" :checked="1== current" color="#FFCC33" style="transform:scale(0.7); margin: auto;" @click="radioChange(1)" />
				</view>
			</view>
			<view style="padding: 20rpx 30rpx;">
				<view class="user_info">
					<image src="../../static/demo/1.jpg"></image>
					<view>
						<view>张三</view>
						<view style="font-size: 28rpx;">深圳南山区</view>
					</view>
					<view class="question_time" style="font-size: 28rpx; ">2020/01/16</view>
				</view>
				<view style="    display: flex;">
					<view style="font-size: 32rpx; padding-left: 40rpx;margin-top: 40rpx;">现在失业，没有方向，该怎么办？</view>
					<radio value="r1" :checked="2 == current" color="#FFCC33" style="transform:scale(0.7); margin: auto;" @click="radioChange(2)"/>
				</view>
			</view>
			<view style="padding: 20rpx 30rpx;">
				<view class="user_info">
					<image src="../../static/demo/1.jpg"></image>
					<view>
						<view>张三</view>
						<view style="font-size: 28rpx;">深圳南山区</view>
					</view>
					<view class="question_time" style="font-size: 28rpx; ">2020/01/16</view>
				</view>
				<view style="    display: flex;">
					<view style="font-size: 32rpx; padding-left: 40rpx;margin-top: 40rpx;">现在失业，没有方向，该怎么办？</view>
					<radio value="r1" :checked="3 == current" color="#FFCC33" style="transform:scale(0.7); margin: auto;" @click="radioChange(3)"/>
				</view>
			</view>
			<view class="input_box">
				<view class="name required">见面地址</view>
				<view class="select_info" @click="popupShow = true">
					<text class="value" v-if="position.length == 3">{{ position[0].name }}{{ position[1].name }}{{ position[2].name }}</text>
					<text class="value" v-else-if="position.length == 2">{{ position[0].name }}{{ position[1].name }}</text>
					<text class="value" v-else-if="position.length == 1">{{ position[0].name }}</text>
					<text class="select" v-else="">请选择地址</text>
				</view>
			</view>
			<view class="input_box btm_line">
				<view class="name required">约见时间</view>
					<picker mode="date" :value="teach.startTime" :start="startDate" :end="endDate" @change="bindDateChange">
					   <view class="select_info">
					   	<view class="value" v-if="teach.startTime">{{ teach.startTime }}</view>
					   	<view class="select" v-else>请选择</view>
					   </view>
					</picker>
			</view>
			<view class="input_box btm_line">
				<view class="name required">时长</view>
				<picker :range="timeData" @change="onPickerChange">
					<view class="select_info">
						<view class="value" v-if="teach.duration">{{ teach.duration }}</view>
						<view class="select" v-else>请选择</view>
					</view>
				</picker>
			</view>
			<view class="input_box">
				<view class="name">备注</view>
				<view class="textarea_info"><textarea v-model="teach.remarks" placeholder="备注信息"></textarea></view>
			</view>
		</view>
		<!-- 按钮 -->
		<view class="form_but"><button class="active" @click="onSubmit(0)">发布</button></view>
		<address-popup v-model="popupShow" :length="3" :force="false"  @change="addressChange"></address-popup>
	</view>
</template>

<script>
	import addressPopup from '@/components/common/address-popup';
	export default {
		components: {
			addressPopup
		},
		data() {
			return {
				teach:{
					startTime:'',
					studyId:'664f93b07e844429844f44ae1c2e5111',
					//endTime:'',
					duration:'',
					type:1,
					address:'',
					remarks:''
				},
				r1:'',
				current: 0,
				timeData:["0.5 小时","1 小时","1.5 小时","2 小时","2.5 小时","3 小时"],
				position:[], // 保存选择的地区
				popupShow: false,
			};
		},
		computed: {
			startDate() {
				return this.getDate('start');
			},
			endDate() {
				return this.getDate('end');
			}
		},
		//页面显示
		onShow() {},
		//方法
		methods: {
			//选择时长
			onPickerChange(e) {
				this.teach.duration = this.timeData[e.detail.value];
			},
			// 选择见面地址
			addressChange(e) {
				console.log(e);
				this.position = e;
			},
			// 选择时间
			bindDateChange(e) {
				this.teach.startTime = e.target.value
			},
			radioChange(val) {
				console.info(val);
				this.current=val;
			},
			moreInfo(){
				// todo 没有跳转 懵逼ing
				console.info("study-info");
			// uni.navigateTo({
			//     url: '/pages/mine/user-info'
			// });
				uni.navigateTo({
				    url: '/pages/add/study-info'
				})
			},
			getDate(type) {
				const date = new Date();
				let year = date.getFullYear();
				let month = date.getMonth() + 1;
				let day = date.getDate();
	
				if (type === 'start') {
					year = year - 60;
				} else if (type === 'end') {
					year = year + 2;
				}
				month = month > 9 ? month : '0' + month;;
				day = day > 9 ? day : '0' + day;
				return `${year}-${month}-${day}`;
			},
			//提交
			onSubmit(state) {
				if (this.teach.startTime == '') {
					uni.showToast({
						title: '请输入问题',
						icon: 'none'
					});
					return;
				}
				this.teach.address = "";
				this.position.forEach(item =>{
					if(this.teach.address == ""){
						this.teach.address += item.name;
					}else{
						this.teach.address += "."+ item.name;
					}
				})
				console.info("submit")
				this.$http
					.post('teach', this.teach)
					.then(res => {
						console.info("result:",res)
						uni.showToast({
							title: '保存成功！'
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

<style lang="scss" scoped>
	@import '@/style/mixin.scss';
.user_info{
	display: flex;
	image{
		margin-right: 10px;
		width: 50px;
		height: 50px;
		border-radius: 50%;
		overflow: hidden;
	}
	.question_time{
		margin: auto;
		position: relative;
		left: 42px;
	}
}
</style>