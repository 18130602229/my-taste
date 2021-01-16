<template>
	<view class="page">
		<nav-bar title="学习" bgColor="#F5f5f5"></nav-bar>
		<view class="input_form_box">
			<view class="input_box btm_line">
				<view class="name required">问题</view>
				<view class="input_info"><input type="text" v-model="study.title" placeholder="请输入" /></view>
			</view>
			<view class="input_box">
				<view class="name required">描述</view>
				<view class="textarea_info"><textarea v-model="study.described" placeholder="请输入问题背景和自己了解情况"></textarea></view>
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
				<view class="input_info"><input v-model="study.type" type="text" placeholder="请输入问题类型" /></view>
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
					<picker mode="date" :value="study.time" :start="startDate" :end="endDate" @change="bindDateChange">
					   <view class="select_info">
					   	<view class="value" v-if="study.time">{{ study.time }}</view>
					   	<view class="select" v-else>请选择</view>
					   </view>
					</picker>
			</view>
		</view>
		
	</view>
</template>

<script>
	import addressPopup from '@/components/common/address-popup';
	export default {
		components: {
			addressPopup
		},
		data() {
			const currentDate = this.getDate({
			            format: true
			        })
			return {
				study:{
					title:'',
					described:'',
					difficultyFactor:'',
					type:'',
					time:'',
					address:'',
					state:''
				},
				difficultyFactor:'',// 显示难度系数 文字描述
				difficultyLevel:["低","中","高"],
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
			//问题难度系数选择
			onPickerChange(e) {
				this.study.difficultyFactor = e.detail.value+1;
				this.difficultyFactor = this.difficultyLevel[e.detail.value];
			},
			// 选择见面地址
			addressChange(e) {
				console.log(e);
				this.position = e;
			},
			// 选择时间
			bindDateChange(e) {
				this.study.time = e.target.value
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
				if (this.study.title == '') {
					uni.showToast({
						title: '请输入问题',
						icon: 'none'
					});
					return;
				}
				this.study.state = state;
				this.study.address = "";
				this.position.forEach(item =>{
					if(this.study.address == ""){
						this.study.address += item.name;
					}else{
						this.study.address += "."+ item.name;
					}
				
				})
				console.info("submit")
				this.$http
					.post('study', this.study)
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

<style lang="scss" scoped>
	@import '@/style/mixin.scss';

</style>
