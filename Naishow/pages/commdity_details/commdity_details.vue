<template>
	<view class="big">
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" class="swiper">
			<swiper-item v-for="(item,index) in slideshow" :key="index">
				<image :src="item.slideshow" class="swiperimg"></image>
			</swiper-item>
		</swiper>
		<view class="blurb">
			<text class="price">￥{{commdity.price}}.00</text>
			<view class="">
				<text class="intro">{{commdity.intro}}</text>
			</view>
			<view class="youzan">
				<image src="https://s1.ax1x.com/2020/05/07/YmKmjK.png" class="youzanimg"></image>
				<text>全程护航，请放心购买</text>
			</view>
		</view>
		<view class="mid">
			<view class="freight">
				<view class="left">
					<text class="yunfei">运费：</text>
					<text>免运费</text>
				</view>
				<view class="right">
					<text>剩余 {{commdity.num}}</text>
				</view>
			</view>
			<view class="freight">
				<view class="left">
					<text class="yunfei">运费：</text>
					<text>收货后结算·快递发货</text>
				</view>
				<view class="right">
					<van-icon name="arrow" />
				</view>
			</view>
		</view>
		<van-goods-action>
			<van-goods-action-icon icon="chat-o" text="客服" dot color="#94D098" />
			<van-goods-action-icon icon="shop-o" text="店铺" />
			<van-goods-action-icon icon="cart-o" text="购物车" :info="comnum" @click="shop" />
			<van-goods-action-button text="加入购物车" type="warning" color="#E1F4E3" text-class="#6CBE72" @click="shopping" />
			<van-goods-action-button text="立即购买" color="#6CBE72" @click="buy" />
		</van-goods-action>
		<view class="popup">
			<van-popup :show="show" round position="bottom" custom-style="height: 40%" @close="onClose" closeable >
				<view class="poptop">
					<view class="pop1">
						<image :src="popupimg" class="popimg"></image>
					</view>
					<view class="pop2">
						<text style="font-size: 40upx;font-weight: bold;color: #6EBF74;">￥{{commdity.price}}.00</text>
						<view style="color: #969799;font-size: 28upx;">剩余<text style="color: red;">{{commdity.num}}</text>件</view>
					</view>
				</view>
				<view class="num">
					<view class="buynum">
						<text>购买数量:</text>
					</view>
					<view class="">
						<van-stepper value="1" min="1" :max="commdity.num" @change="onChange" />
					</view>
				</view>
				<view class="next">
					<van-button type="large" color="#6CBE72" round @click="next">{{but}}</van-button>
				</view>
			</van-popup>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				commdity: [], //商品
				slideshow: [], //轮播
				show: false,
				popupimg:'',
				step:1,
				comnum:'',
				but:''
			}
		},
		onLoad(news) {
			// console.log(news)
			var item = JSON.parse(decodeURIComponent(news.news));
			console.log(item)
			this.commdity = item;
			this.slideshow = item.slideshow
			console.log(this.slideshow)
			this.popupimg = item.slideshow[0].slideshow
			// this.comnum = uni.getStorageSync('comnum')
		},
		methods: {
			buy() {
				this.show = !this.show;
				this.but = '下一步';
			},
			onClose() {
				this.show = false
			},
			onChange(event) {
			    console.log(event.detail);
				this.step = event.detail;
			},
			next(){
				if(this.but == '加入购物车'){
					var commdity = this.commdity;
					var steps = this.step;
					var that = this;
					this.show = true;
					this.but = '加入购物车';
					let commlist = uni.getStorageSync('commlist');
					console.log(commlist)
					var comm={
						pid:this.commdity.pid,
						intro:this.commdity.intro,
						price:this.commdity.price,
						img:this.commdity.img,
						step:steps,
						check:false
					};
					var s = 0;
						for(let c in commlist){
							if(commlist[c].pid == comm.pid){
								s = 1;
								commlist[c].step += comm.step;
								break;
							}else{
								s = 0;
							}
						}
						if (s == 0){
							commlist.push(comm)
						}
					console.log(commlist)
					this.comnum = commlist.length
					uni.setStorageSync('comnum',commlist.length)
					uni.setStorageSync('commlist',commlist)
					uni.setStorageSync('steps',steps)
					uni.showToast({
					    title: '添加购物车成功',
					    duration: 2000
					});
					this.show = false;
				}else{
					// var commdity = JSON.stringify(this.commdity);
					var commdity = this.commdity;
					var steps = this.step;
					uni.setStorageSync('comm',commdity)
					uni.setStorageSync('steps',steps)
					uni.navigateTo({
						url:'../ack_order/ack_order'
					})
				}
			},
			shop(){
				uni.switchTab({
					url:'../shopping/shopping'
				})
			},
			shopping(){
				this.show = true;
				this.but = '加入购物车';
				// var commdity = this.commdity;
				// var steps = this.step;
				// var that = this;
				
				// let commlist = uni.getStorageSync('commlist');
				// console.log(commlist)
				// var comm={
				// 	pid:this.commdity.pid,
				// 	intro:this.commdity.intro,
				// 	price:this.commdity.price,
				// 	img:this.commdity.img,
				// 	step:steps,
				// 	check:false
				// };
				// var s = 0;
				// 	for(let c in commlist){
				// 		if(commlist[c].pid == comm.pid){
				// 			s = 1;
				// 			commlist[c].step = comm.step;
				// 			break;
				// 		}else{
				// 			s = 0;
				// 		}
				// 	}
				// 	if (s == 0){
				// 		commlist.push(comm)
				// 	}
				// console.log(commlist)
				// uni.setStorageSync('commlist',commlist)
				// uni.setStorageSync('steps',steps)
				// uni.showToast({
				//     title: '添加购物车成功',
				//     duration: 2000
				// });
			}
		}
	}
</script>

<style>
	.big {
		height: 2200upx;
	}

	.swiper {
		width: 100%;
		height: 900upx;
	}

	.swiperimg {
		width: 100%;
		height: 900upx;
	}

	.price {
		font-size: 38upx;
		color: #6CBE72;
		font-weight: bold;
		margin: 3%;
	}

	.intro {
		font-size: 34upx;
		margin: 3%;
	}

	.youzan {
		display: flex;
		margin: 5% 3%;
	}

	.youzanimg {
		width: 25%;
		height: 50upx;
	}

	.youzan text {
		color: #646566;
		margin: 0 0 0 5%;
	}

	.mid {
		width: 100%;
		height: 200upx;
		background-color: #F9F9F9;
	}

	.freight {
		width: 100%;
		height: 80upx;
		background-color: #FFFFFF;
		margin: 3% 0;
		display: flex;
		justify-content: space-between;
		font-size: 34rpx;
	}

	.left {
		margin: 2% 0 0 3%;
	}

	.right {
		margin: 2% 3% 0 0;
		color: #A5A6A8;
	}

	.yunfei {
		color: #A5A6A8;
	}
	.popimg{
		width: 100%;
		height: 200upx;
		margin: 5%;
	}
	.poptop{
		display: flex;
		
	}
	.pop1{
		width: 30%;
		height: 200upx;
	}
	.pop2{
		width: 70%;
		height: 200upx;
		margin: 15% 0 0 5%;
	}
	.num{
		display: flex;
		justify-content: space-between;
		margin: -5% 0 0 0;
	}
	.buynum{
		margin: 0 0 0 5%;
	}
	.next{
		margin: 5% 0 0 5%;
		width: 90%;
	}
</style>
