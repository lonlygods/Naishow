<template>
	<view>
		<view class="site" @click="site" v-if="userName =='' ">
			<view class="left">
				<view class="jia">
					<van-icon name="plus" color="white" size="40px" />
				</view>
			</view>
			<view class="siz">
				<text>选择收货地址</text>
			</view>
			<view class="right">
				<van-icon name="arrow" color="#9B9C9E" size="20px" />
			</view>
		</view>
		<view class="site2" @click="site" v-else>
			<view class="site_content">
				<text style="font-weight: bold;padding: 0 1%;">收货人:{{userName}}</text>
				<text>{{telNumber}}</text>
				<text>\n</text>
				<text>收货地址:{{carmodel}}</text>
				<text>{{detailInfo}}</text>
			</view>
		</view>
		<view class="dashedBorder"></view>
		<view class="commdity_msg">
			<view class="title">
				<van-icon name="shop-o" color="#5D5D5E" size="20px" />
				<text>奈雪の茶</text>
			</view>
			<view class="msg">
				<view class="msg1">
					<image :src="popupimg" class="msgbig"></image>
				</view>
				<view class="right2">
					<text class="msgsize">{{commdity.intro}}</text>
					<view class="price_num">
						<text style="color: #6CBE72;font-weight: bold;">￥{{commdity.price}}.00</text>
						<text style="color: #363637;font-size: 28upx;">× {{step}}</text>
					</view>
				</view>
			</view>
		</view>
		<view class="onsale">
			<view class="saleleft">
				<text>优惠</text>
			</view>
			<view class="saleright">
				<text>暂无可用</text>
				<van-icon name="arrow" color="#9B9C9E" size="18px" />
			</view>
		</view>
		<view class="onsale2">
			<view class="saleleft">
				<text>配送方式</text>
			</view>
			<view class="saleright">
				<text>快递</text>
			</view>
		</view>
		<view class="">
			<van-cell-group>
				<van-field value="" clearable label="买家留言"  placeholder="留言建议提前协商(50字以内)" @click-icon="onClickIcon" custom-style="font-size:36upx;" />
			</van-cell-group>
		</view>
		<view class="onsale3">
			<view class="saleleft">
				<text>商品金额</text>
			</view>
			<view class="saleright">
				<text style="font-size: 28upx;">￥{{commdity.price}}.00</text>
			</view>
		</view>
		<text class="tatol">合计：<text style="color: #6CBE72;">{{total}}.00</text></text>
		<view class="bottom_total">
			<text class="bottom2">合计：<text style="color: #6CBE72;">{{total}}.00</text></text>
			<view class="submit">
				<van-button type="primary" size="normal">确认订单</van-button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				commdity: [],
				step: '',
				popupimg: '',
				total:'',
				acksite:true,
				acksite2:true,
				userName:'',
				telNumber:'',
				detailInfo:'',
				carmodel:''
			}
		},
		onLoad(option) {
			console.log(option)
			//默认地址
			this.userName = option.userName;
			this.telNumber = option.telNumber;
			this.carmodel = option.carmodel;
			this.detailInfo = option.detailInfo;
			//商品信息
			var commdity = uni.getStorageSync('comm');
			var step = uni.getStorageSync('steps');
			console.log(step)
			console.log(commdity)
			this.commdity = commdity
			this.step = step
			this.popupimg = commdity.slideshow[0].slideshow
			this.total = commdity.price * this.step
			console.log(this.total)
			
			if(this.userName !== ''){
				this.acksite = false;
				this.acksite2 = true
			}else{
				this.acksite2 = false;
				this.acksite = true
			}
		},
		methods: {
			site(){
				uni.navigateTo({
					url:'../site/site'
				})
			}
		}
	}
</script>

<style>
	.site {
		width: 100%;
		display: flex;
		justify-content: space-between;
	}

	.jia {
		width: 80upx;
		height: 80upx;
		background-color: #3388FF;
		border-radius: 10%;
		margin: 10%;
	}

	.siz {
		margin: 3% 0 0 -50%;
	}

	.right {
		margin: 3% 0 0 0;
	}

	.dashedBorder {
		height: 4upx;
		background: linear-gradient(to right, #FF6D6D, #3283FA 18px, transparent 18px, transparent);
		background-size: 30px 100%;
		margin: 3% 0 0 0;
	}

	.title {
		display: flex;
		color: #5D5D5E;
		font-size: 36upx;
		margin: 5%;
	}

	.msg {
		width: 100%;
		height: 80upx;
		background-color: #FFFFFF;
		margin: 3% 0;
		display: flex;
		justify-content: space-between;
		font-size: 34rpx;
	}

	.msg1 {
		width: 35%;
		height: 220upx;
	}

	.msgbig {
		width: 90%;
		height: 220upx;
		margin: 0 5%;
		border-radius: 20upx;
	}

	.right2 {
		width: 65%;
	}

	.msgsize {
		width: 90%;
		font-size: 32upx;
		margin: 0 0 0 5%;
	}

	.price_num {
		display: flex;
		justify-content: space-between;
		margin: 15% 0 0 0;
	}

	.onsale {
		width: 100%;
		height: 100upx;
		display: flex;
		justify-content: space-between;
		margin: 30% 0 0 0;
		font-size: 36upx;
	}

	.onsale2 {
		width: 100%;
		height: 100upx;
		display: flex;
		justify-content: space-between;
		font-size: 36upx;
	}
	.onsale3{
		width: 100%;
		height: 100upx;
		display: flex;
		justify-content: space-between;
		font-size: 32upx;
		margin: 5% 0 0 0;
	}
	.saleleft{
		margin: 0 0 0 5%;
	}
	.saleright{
		margin: 0 3% 0 0;
	}
	.tatol{
		font-size: 34upx;
		float: right;
		margin: -5% 3% 0 0;
	}
	.bottom_total{
		width: 100%;
		height: 120upx;
		position: absolute;
		margin: 15% 0 0 0;
		background-color: white;
		display: flex;
		justify-content: flex-end;
		  align-items: flex-end;
	}
	.bottom2{
		font-size: 36upx;
		font-weight: bold;
		margin: 3% 0 3% 0;
	}
	.site2{
	  width: 100%;
	  /* height: 100rpx; */
	  /* border-bottom: solid 3rpx #EAEAEA; */
	}
	.site2 text{
	  margin: 40rpx 0 0 0%;
	  /* padding: 0 1%; */
	}
	.site_content{
	  margin: 5% 0 0 0;
	}
</style>
