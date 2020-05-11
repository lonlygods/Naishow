<template>
	<view class="big">
		<view class="head">
			<image src="https://s1.ax1x.com/2020/05/10/Y3Yfzt.png"></image>
			<text class="naitext">奈雪の茶</text>
			<view class="order1">
				<view class="orderleft1">
					<text>公告：欢迎光临本店！</text>
				</view>
				<view class="orderright1">
					<text>更多优惠</text>
					<van-icon name="arrow" />
				</view>
			</view>
			<view class="index" @click="index">
				<view class="home">
					<view class="orderleft">
						<text style="color: #666666;">店铺首页</text>
					</view>
					<view class="orderright">
						<van-icon name="arrow" />
					</view>
				</view>
			</view>
		</view>
		<view class="edge">
			<van-sidebar :active-key="activeKey" class="activ">
				<van-sidebar-item :title="item.name" @click="lick" v-for="(item,index) in list" :key="index" />
			</van-sidebar>
		</view>
		<view class="com" @click="li">
			<view class="commdity" v-for="(com,index) in commdity" :key="com.id">
				<image :src="com.photo"></image>
				<text class="name">{{com.name}}</text>
				<text class="price">￥{{com.price}}.00<text style="font-size: 12px;">起</text></text>
				<van-stepper :value="com.num" @change="onChange" input-width="30px" button-size="25px" :data-index="index" class="step"
				 min="0" max="10" />
			</view>
		</view>
		<view class="but" v-show="but" @click="butt">
			<view class="shop">
				<!-- <image src="https://s1.ax1x.com/2020/05/10/Y3IcGj.png" class="logo"></image> -->
				<van-image round width="3rem" height="3rem" src="https://s1.ax1x.com/2020/05/10/Y3IcGj.png" class="logo" />
				<van-tag round color="#FF4444" text-color="#FFFFFF" style="margin: -5% 0 0 -3%;">{{totalnum}}</van-tag>
				<text class="total"><text style="color: #A3A3A3;">合计：</text>￥{{total}}.00</text>
				<view class="rig">
					<van-button type="danger" size="large">去结算</van-button>
				</view>
			</view>
		</view>
		<view class="pull" v-show="show">
			<view class="pulltop">
				<text>购物车</text>
			</view>
			<view class="shopdetails" v-for="(shopcom,index) in commdity" :key="shopcom.id" v-if="shopcom.num">
				<text class="pullname">{{shopcom.name}}</text>
				<text class="pullprice">￥{{shopcom.price}}.00</text>
				<van-stepper :value="shopcom.num" @change="onChange" :data-index="index" min="0" max="10" class="tstep" />
			</view>
			<!-- <van-popup :show="show" closeable position="bottom" custom-style="height: 20%" @close="onClose" /> -->
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				activeKey: 0,
				list: [{
						id: 1,
						name: '零食类'
					},
					{
						id: 2,
						name: '创意类'
					},
					{
						id: 3,
						name: '心意卡'
					},
					{
						id: 4,
						name: '茶礼盒'
					},
					{
						id: 5,
						name: '蛋糕类'
					}
				],
				commdity: [{
						id: 1,
						name: '奈雪 冻干酸奶块 可以嚼的浓缩营养',
						price: '16',
						photo: 'https://s1.ax1x.com/2020/05/10/Y3yUFP.png',
						num: 0
					},
					{
						id: 2,
						name: '奈雪 冻干水果系列 草莓苹果/榴莲/混合水果',
						price: '16',
						photo: 'https://s1.ax1x.com/2020/05/10/Y3ytot.png',
						num: 0
					},
					{
						id: 3,
						name: '奈雪 冻干草莓/榴莲巧克力甜品零食',
						price: '38',
						photo: 'https://s1.ax1x.com/2020/05/10/Y3yYdI.png',
						num: 0
					},
					{
						id: 4,
						name: '奈雪 蔓越莓摩卡西饼休闲零食点心',
						price: '20',
						photo: 'https://s1.ax1x.com/2020/05/10/Y3y8Ld.png',
						num: 0
					},
					{
						id: 5,
						name: '奈雪 薯条 "薯"于你的吮指美味听得见的酥脆·薯条',
						price: '18',
						photo: 'https://s1.ax1x.com/2020/05/10/Y3yJeA.png',
						num: 0
					}
				],
				but: true,
				show: false,
				total: '0',
				totalnum: '0'
			}
		},
		methods: {
			index() {
				uni.switchTab({
					url: '../index/index'
				})
			},
			li() {
				this.show = false;
			},
			//侧边导航
			lick(event) {
				var that = this
				// console.log(event.detail)
				console.log(that.commdity)
				this.show = false;
			},
			//步进器
			onChange(event) {
				// console.log(event.detail);
				console.log(event.currentTarget.dataset.index)
				this.commdity[event.currentTarget.dataset.index].num = event.detail;
				// console.log(this.commdity)
				this.step()
				if (this.totalnum == 0) {
					this.show = false;
				}
			},
			step() {
				var totalnum = 0;
				var total = 0;
				for (let c in this.commdity) {
					totalnum += this.commdity[c].num
					total += this.commdity[c].price * this.commdity[c].num
				}
				console.log('总数量：' + totalnum)
				// console.log(total)
				this.total = total;
				this.totalnum = totalnum;
			},
			onClose() {
				this.show = false;
			},
			butt(){
				this.show = !this.show ;
			}
		}
	}
</script>

<style>
	.big {
		height: 1200rpx;
	}

	.edge {
		position: fixed;
		top: 200upx;
		left: 0;
	}

	.activ {
		width: 20%;
	}

	.head {
		width: 100%;
		height: 200upx;
		position: fixed;
		top: 0;
		background-color: #FFFFFF;
		border-bottom: solid 1px #F3F3F3;
		z-index: 20;
	}

	.head image {
		width: 100upx;
		height: 100upx;
		margin: 3%;
	}

	.naitext {
		font-size: 36upx;
		font-weight: bold;
		position: absolute;
		margin: 3% 0 0 0;
	}

	.order1 {
		width: 80%;
		display: flex;
		justify-content: space-between;
		line-height: 80upx;
		margin: -12% 0 0 17%;
		font-size: 28upx;
	}

	.orderleft1 {
		color: #9FA0A2;
		margin: 0 0 0 3%;
	}

	.orderright1 {
		color: #9FA0A2;
	}

	.index {
		width: 100%;
	}

	.home {
		width: 80%;
		display: flex;
		justify-content: space-between;
		line-height: 80upx;
		margin: -2% 0 0 0;
		font-size: 28upx;
	}
	.orderleft{
		margin: 0 0 0 4%; 
	}

	.com {
		width: 70%;
		height: 120px;
		margin: 25% 0 0 23%;
	}

	.commdity {
		width: 100%;
		height: 200upx;
	}

	.commdity image {
		width: 100px;
		height: 100px;
	}

	.name {
		position: absolute;
		margin: 2% 0 0 3%;
		font-size: 30rpx;
	}

	.price {
		font-size: 32rpx;
		color: #E02D3F;
		/* position: absolute; */
		margin: -3% 0 0 2%;
	}

	.step {
		position: absolute;
		margin: 20% 0 0 0;
		right: 0;
	}

	.but {
		width: 100%;
		height: 90upx;
		bottom: 0;
		position: fixed;
		background-color: #FFFFFF;
		color: #0F0F0F;
		border-top: solid 1px #F3F3F3;
		z-index: 4;
	}

	.shop {
		display: flex;
	}

	.logo {
		/* width: 130upx;
		height: 110upx; */
		margin: -3% 0 0 3%;
	}

	.total {
		width: 45%;
		font-size: 28rpx;
		color: #0F0F0F;
		font-weight: bold;
		margin: 5%;
	}

	.rig {
		width: 30%;
		border-left: solid 1px #FFFFFF;
		margin: 0 0 0 22%;
	}

	.xuanhaole {
		font-size: 40rpx;
		color: #FFFFFF;
		position: relative;
		top: 5%;
		left: 40%;
	}

	.order {
		font-size: 30rpx;
		position: relative;
		top: 40%;
		right: 5%;
	}

	.pull {
		width: 100%;
		height: auto;
		background-color: #FFFFFF;
		bottom: 5%;
		position: fixed;
		z-index: 3;
		overflow: auto;
	}
	.pull::-webkit-scrollbar {
		border-width:1px;
	}
	.shopdetails {
		height: 30px;
		display: flex;
		margin: 2% 0;
		/* justify-content: space-around; */
	}

	.tstep {
		position: absolute;
		right: 0;
	}
	.pullname{
		font-size: 32rpx;
		position: absolute;
		margin: 0 0 0 5%;
		width: 45%;
		text-overflow:ellipsis;
		overflow:hidden; 
		white-space:nowrap;
	}
	.pullprice{
		color: #E02D3F;
		position: absolute;
		margin: 0 0 0 50%;
		font-size: 32rpx;
	}
	.pulltop{
		width: 100%;
		height: 60upx;
		font-size: 34upx;
		line-height: 20px;
		font-weight: bold;
		border-left: solid 8upx #E02D3F;
		border-bottom: solid 3upx #F2F2F2;
	}
	.pulltop text{
		display: inline-block;
		margin:2% 0 0 3%;
	}
</style>
