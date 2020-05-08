<template>
	<view>
		<view @click="site" class="wxsite">
			<view class="wxleft">
				<image src="https://s1.ax1x.com/2020/05/07/Ye0zrQ.png" class="wechat"></image>
				<text>获取微信收货地址</text>
			</view>
			<view class="wxright">
				<van-icon name="arrow" color="#9B9C9E" size="25px" />
			</view>
		</view>
		<view class="">
			<van-cell-group>
				<van-field :value="userName" clearable label="收货人" icon="question-o" placeholder="收货人姓名"
				 @click-icon="onClickIcon" :error-message="nameMessage" @change="nameChange" />
				<van-field :value="telNumber" label="手机号码" placeholder="收货人手机号" border="false" :error-message="phoneMessage" @change="telChange" />
				<view class="danyuan" @click="show = true">
					<view>省/市/区</view>
					<input type="text" placeholder="选择省/市/区" :value="carmodel" class="uni-input" />
				</view>
				<van-popup :show="show" @close="onClose" position="bottom" custom-style="height: 50%;">
					<van-area :area-list="areaList" @confirm="queren" @cancel="quxiao" />
				</van-popup>
				<van-field :value="detailInfo" label="收货地址" placeholder="请填写收货地址" border="false" @change="detailClick" />
			</van-cell-group>
		</view>
		<van-button class="dibu" type="primary" size="large" color="#6CBE72" @click="add">保存并使用</van-button>
	</view>
</template>

<script>
	import AreaList from '@/static/area.js'
	export default {
		data() {
			return {
				show: false,
				areaList: AreaList,
				carmodel:'',
				userName:'',
				telNumber:'',
				provinceName:'',
				cityName:'',
				countyName:'',
				detailInfo:'',
				nameMessage: '',
				phoneMessage: ''
			}
		},
		onLoad() {
			// console.log(AreaList)
		},
		methods: {
			site() {
				var that = this;
				uni.chooseAddress({
				  success(res) {
				    console.log(res)
					that.userName = res.userName;
					that.telNumber = res.telNumber;
					// that.provinceName = res.provinceName;
					// that.countyName = res.countyName;
					// that.cityName = res.cityName;
					that.carmodel = res.provinceName +' '+res.countyName+' '+res.cityName; //微信收货地址省市区对应vant转换
					that.detailInfo = res.detailInfo;
				  }
				})
			},
			showPopup() {
			    this.show = true;
			  },
			  onClose() {
			    this.show = false;
			  },
			  queren(suc){
				  console.log(suc)
				  // for(var s in suc.detail.values){
					 //  this.carmodel += suc.detail.values[s].name + ' '
				  // }
				  //vant省市区拼接
				  this.carmodel = suc.detail.values[0].name+' '+ suc.detail.values[1].name+' '+ suc.detail.values[2].name
				  this.show = false;
			  },
			  quxiao(){
				  this.show = false;
			  },
			  // 验证姓名
			  nameChange: function(event) {
			  	let name = event.detail
			  	let message = '';
			  	if (name) {
			  		if (/^[\u4e00-\u9fa5]{2,6}$/.test(name)) {
			  			message = '';
			  		} else {
			  			message = '您输入的姓名有误';
			  		}
			  	} else {
			  		message = '输入的姓名不能为空';
			  	};
			  	this.nameMessage = message;
			  	this.name = name;
				this.userName = name;
			  },
			  // 验证手机号
			  telChange: function(event) {
			  	let phone = event.detail
			  	// console.log(event)
			  	let message = '';
			  	if (phone) {
			  		if (/^1(3|4|5|7|8)\d{9}$/.test(phone)) {
			  			message = '';
			  		} else {
			  			message = '您输入的手机号码有误';
			  		}
			  	} else {
			  		message = '输入的手机号不能为空'
			  	};
			  	this.phoneMessage = message;
			  	this.phone = phone;
			  	// console.log(this.phone)
				this.telNumber = phone;
			  },
			  detailClick: function(event) {
			  	this.detailInfo = event.detail;
			  	// console.log(this.address)
				this.detailInfo = event.detail;
			  },
			  add(){
				this.detailInfo = this.carmodel + this.detailInfo;
			  	uni.navigateTo({
			  		url:'../site/site?userName='+ this.userName+"&telNumber="+ this.telNumber+"&detailInfo="+ this.detailInfo,
					animationType: 'pop-in',
					animationDuration: 200
			  	})
			  }
		}
	}
</script>

<style>
	.wxsite {
		width: 100%;
		height: 100upx;
		display: flex;
		justify-content: space-between;
		background-color: #FCFCFC;
	}

	.wechat {
		width: 50upx;
		height: 50upx;
	}

	.wxleft {
		margin: 5% 0 0 5%;
	}

	.wxleft text {
		position: absolute;
		top: 38upx;
	}

	.wxright {
		margin: 5% 5% 0 0;
	}

	.check {
		position: absolute;
		margin: 2% 0 0 0;
	}
	.danyuan{
		padding: 1% 4%;
		display: flex;
		font-size: 14px;
		height: 30px;
		border-bottom: solid 1rpx #F4F5F6;
	}
	.danyuan view{
		width: 23%;
	}
	.dibu{
		position: fixed;
		width: 100%;
		bottom: 0;
	}
</style>
