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
		<view class="site" @click="picksite">
			<!-- <van-checkbox :value="checked" checked-color="#6CBE72" @change="onChange" class="check"></van-checkbox> -->
			<view class="site_content">
				<text>{{userName}}</text>
				<text>{{telNumber}}</text>
				<text>\n</text>
				<text>{{provinceName}}{{cityName}}{{countyName}}{{detailInfo}}</text>
			</view>
		</view>
		<van-button class="dibu" type="primary" size="large" color="#6CBE72" @click="add">新增收货地址</van-button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userName: '',
				telNumber: '',
				provinceName: '',
				cityName: '',
				countyName: '',
				detailInfo: '',
				checked: true,
				carmodel: ''
			}
		},
		onLoad(option) {
			console.log(option)
			this.userName = option.userName;
			this.telNumber = option.telNumber;
			this.detailInfo = option.detailInfo;
			console.log(this.userName)
			console.log(this.telNumber)
			console.log(this.detailInfo)
		},
		methods: {
			site() {
				var that = this;
				uni.chooseAddress({
					success(res) {
						console.log(res)
						that.userName = res.userName;
						that.telNumber = res.telNumber;
						that.provinceName = res.provinceName;
						that.countyName = res.countyName;
						that.cityName = res.cityName;
						that.detailInfo = res.detailInfo;
						that.carmodel = res.provinceName + ' ' + res.countyName + ' ' + res.cityName; //微信收货地址省市区对应vant转换
					}
				})
			},
			onChange(event) {
				this.checked = event.detail
			},
			add() {
				uni.navigateTo({
					url: '../add_site/add_site'
				})
			},
			picksite() {
				uni.navigateTo({
					url: '../ack_order/ack_order?userName=' + this.userName + "&telNumber=" + this.telNumber + "&detailInfo=" + this.detailInfo + "&carmodel=" + this.carmodel,
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

	.site {
		width: 90%;
		height: 110upx;
		/* border-bottom: solid 3rpx #F2F2F2; */
		margin: 0 5%;
	}

	.site_content {
		margin: 2% 5%;
	}

	.site_content text {
		padding: 0 2%;
	}

	.edit {
		position: absolute;
		margin: -10% 0 0% 82%;
	}

	.dibu {
		position: fixed;
		width: 100%;
		bottom: 0;
	}
</style>
