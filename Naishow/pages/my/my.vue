<template>
	<view class="big">
		<view class="head_context">
			<view class="login" @click="login" v-if="name == ''">
				<van-button type="primary" color="#3F3B34">获取</van-button>
			</view>
			<view class="userinfo" v-else>
				<van-image round width="4.5rem" height="4.5rem" :src="avatarUrl" class="headimg" />
				<text class="name">{{name}}</text>
				<view class="grow">
					<text>成长值0</text>
				</view>
			</view>
			<view class="vip">
				<view class="naishowleft">
					<image src="https://s1.ax1x.com/2020/05/08/YK3LJU.png" class="v"></image>
					<text>奈雪の茶</text>
				</view>
				<view class="naishowright">
					<text>成为会员</text>
					<van-icon name="arrow" />
				</view>
			</view>
		</view>
		<view class="midmoney">
			<van-row gutter="15" style="margin: 0 0 0 15%;">
				<van-col span="5" offset="3">
					<text>0.00</text>
					<text>\n</text>
					<text class="xia">余额</text>
				</van-col>
				<van-col span="5">
					<text>0</text>
					<text>\n</text>
					<text class="xia">积分</text>
				</van-col>
				<van-col span="5">
					<text>0</text>
					<text>\n</text>
					<text class="xia">卡</text>
				</van-col>
				<van-col span="6">
					<text style="margin: 0 0 0 40upx;">0</text>
					<text>\n</text>
					<text class="xia">优惠券/码</text>
				</van-col>
			</van-row>
		</view>
		<view class="mid">
			<view class="order">
				<view class="orderleft">
					<text>我的订单</text>
				</view>
				<view class="orderright">
					<text>查看全部订单</text>
					<van-icon name="arrow" />
				</view>
			</view>
			<view class="grid">
				<van-grid column-num="5">
					<van-grid-item icon="tosend" text="待付款" />
					<van-grid-item icon="paid" text="待发货" />
					<van-grid-item icon="logistics" text="待收货" />
					<van-grid-item icon="smile-comment-o" text="评价" />
					<van-grid-item icon="gold-coin-o" text="退款/售后" />
				</van-grid>
			</view>
		</view>
		<view class="menushop" @click="shop">
			<view class="orderleft">
				<van-icon name="shopping-cart-o" size="25px" />
				<text>购物车</text>
			</view>
			<view class="orderright">
				<van-icon name="arrow" />
			</view>
		</view>
		<view class="shipping" @click="shipping">
			<view class="orderleft">
				<van-icon name="location-o" size="25px" />
				<text>收货地址</text>
			</view>
			<view class="orderright">
				<van-icon name="arrow" />
			</view>
		</view>
		<view class="mymsg">
			<view class="orderleft">
				<van-icon name="contact" size="25px" />
				<text>个人信息</text>
			</view>
			<view class="orderright">
				<van-icon name="arrow" />
			</view>
		</view>
		<view class="user">
			<view class="orderleft">
				<van-icon name="manager-o" size="25px" />
				<text>账号设置</text>
			</view>
			<view class="orderright">
				<van-icon name="arrow" />
			</view>
		</view>
		<image src="https://s1.ax1x.com/2020/05/08/YK2ePS.png" class="bottompic"></image>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				name: '',
				avatarUrl: ''
			}
		},
		onLoad() {

		},
		methods: {
			login() {
				var that = this;
				uni.login({
					provider: 'weixin',
					success: function(loginRes) {
						// console.log(loginRes);
						// 获取用户信息
						uni.getUserInfo({
							provider: 'weixin',
							success: function(infoRes) {
								// console.log(infoRes)
								that.name = infoRes.userInfo.nickName
								that.avatarUrl = infoRes.userInfo.avatarUrl
							}
						});
					}
				});
			},
			shipping(){
				uni.navigateTo({
					url:'../site/site'
				})
			},
			shop(){
				uni.switchTab({
					url:'../shopping/shopping'
				})
			}
		}
	}
</script>

<style>
	.big {
		width: 100%;
		height: 1600upx;
		background-color: #F7F8FA;
		position: absolute;
		top: 0;
	}

	.head_context {
		width: 100%;
		height: 340upx;
		background-color: #BD8E61;
		position: absolute;
		top: 0;
	}

	.login {
		display: flex;
		justify-content: center;
		width: 100%;
		height: 150upx;
	}

	.userinfo {
		width: 100%;
		height: 150upx;
	}

	.headimg {
		display: inline-block;
		margin: 12% 0 0 5%;
	}

	.name {
		font-size: 40upx;
		font-weight: bold;
		color: #333333;
		position: absolute;
		margin: 15% 0 0 3%;
	}

	.grow {
		width: 15%;
		height: 44upx;
		background-color: #3A362F;
		border-radius: 30upx;
		color: #FDDDA5;
		display: flex;
		justify-content: center;
		margin: -8% 0 0 27%;
		font-size: 26upx;
	}

	.vip {
		width: 90%;
		height: 80upx;
		background-color: #38342D;
		border-top-left-radius: 20upx;
		border-top-right-radius: 20upx;
		margin: 15% 0 0 5%;
		/* position: absolute; */
		line-height: 80upx;
	}

	.vip {
		display: flex;
		justify-content: space-between;
	}

	.v {
		width: 40upx;
		height: 40upx;
	}

	.naishowleft {
		color: #FDDC9F;
		margin: 0 0 0 3%;
	}

	.naishowright {
		color: #FFFFFF;
		margin: 0 3% 0 0;
	}

	.midmoney {
		width: 95%;
		height: 140upx;
		background-color: #FFFFFF;
		border-radius: 30upx;
		margin: 50% 0 0 2.5%;
	}

	.xia {
		color: #999999;
	}

	.mid {
		width: 95%;
		height: 250upx;
		background-color: #FFFFFF;
		border-radius: 30upx;
		margin: 5% 0 0 2.5%;
	}

	.order {
		width: 90%;
		height: 80upx;
		display: flex;
		justify-content: space-between;
		border-bottom: solid 2upx #F5F6F8;
		line-height: 80upx;
		margin: 0 0 0 5%;
	}

	.orderleft {
		color: #323233;
		margin: 0 0 0 3%;
	}

	.orderright {
		color: #9FA0A2;
		/* margin: 0 3% 0 0; */
	}

	.menushop {
		width: 95%;
		background-color: #FFFFFF;
		border-radius: 16upx;
		margin: 3% 0 0 2.5%;
		height: 80upx;
		display: flex;
		justify-content: space-between;
		border-bottom: solid 2upx #F5F6F8;
		line-height: 80upx;
	}

	.shipping {
		width: 95%;
		background-color: #FFFFFF;
		border-radius: 16upx;
		margin: 3% 0 0 2.5%;
		height: 80upx;
		display: flex;
		justify-content: space-between;
		border-bottom: solid 2upx #F5F6F8;
		line-height: 80upx;
	}

	.mymsg {
		width: 95%;
		background-color: #FFFFFF;
		border-top-left-radius: 16upx;
		border-top-right-radius: 16upx;
		margin: 3% 0 0 2.5%;
		height: 80upx;
		display: flex;
		justify-content: space-between;
		border-bottom: solid 2upx #F5F6F8;
		line-height: 80upx;
	}

	.user {
		width: 95%;
		background-color: #FFFFFF;
		border-bottom-left-radius: 16upx;
		border-bottom-right-radius: 16upx;
		margin: 0% 0 0 2.5%;
		height: 80upx;
		display: flex;
		justify-content: space-between;
		border-bottom: solid 2upx #F5F6F8;
		line-height: 80upx;
	}

	.bottompic {
		width: 30%;
		height: 100upx;
		margin: 35% 0 0 35%;
	}
</style>
