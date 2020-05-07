<template>
	<view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" class="swiper">
			<swiper-item v-for="(item,index) in swiper" :key="index">
				<image :src="item.img" class="swiperimg"></image>
			</swiper-item>
		</swiper>
		<view class="comm">
			<image src="https://s1.ax1x.com/2020/05/07/YeGLCQ.png" class="coupon"></image>
			<image src="https://s1.ax1x.com/2020/05/07/YeGO3j.png" class="coupon2"></image>
		</view>
		<view class="new">
			<image src="https://s1.ax1x.com/2020/05/07/YeG7E8.png" class="newimg"></image>
			<image src="https://s1.ax1x.com/2020/05/07/YeGIDP.png" class="newbanner"></image>
			<view class="newcomm">
				<view class="newlist" v-for="(n,index) in newcomm" :key="index" @click="news(n)">
					<image :src="n.img" class="newlistimg"></image>
					<view class="new_name">
						<text>{{n.name}}</text>
					</view>
					<view class="new_price">
						<text>￥{{n.price}}</text>
						<van-icon name="shopping-cart-o" color="#6D9263" size="50upx" />
					</view>
				</view>
			</view>
		</view>
		<view class="new">
			<image src="https://s1.ax1x.com/2020/05/07/YeGoHf.png" class="teaimg"></image>
			<image src="https://s1.ax1x.com/2020/05/07/YeG5ut.png" class="newbanner"></image>
			<view class="newcomm">
				<view class="newlist" v-for="(t,index) in teacomm" :key="t.pid" @click="tea(t)">
					<image :src="t.img" class="newlistimg"></image>
					<view class="new_name">
						<text>{{t.name}}</text>
					</view>
					<view class="new_price">
						<text>￥{{t.price}}</text>
						<van-icon name="shopping-cart-o" color="#6D9263" size="50upx" />
					</view>
				</view>
			</view>
		</view>
		<view class="service">
			<image src="https://s1.ax1x.com/2020/05/07/YefYVK.png" class="serv"></image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swiper: [{
						img: 'https://s1.ax1x.com/2020/05/07/Ye8ZW9.png'
					},
					{
						img: 'https://s1.ax1x.com/2020/05/07/Ye8VJJ.png'
					},
					{
						img: 'https://s1.ax1x.com/2020/05/07/Ye8Ei4.png'
					}
				],
				newcomm: [{
						pid: 1,
						img: 'https://s1.ax1x.com/2020/05/07/YeGhjI.png',
						name: '"梅"你不行挂画',
						price: '119',
						intro:'奈雪"梅你不行"主题挂画 夏日杨梅周边',
						primary_price: '149',
						slideshow:[
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye3YrV.png'
							},
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye37sP.png'
							}
						],
						num:'19'
					},
					{
						pid: 2,
						img: 'https://s1.ax1x.com/2020/05/07/YeGW3d.png',
						name: '"梅"你不行托特包',
						price: '99',
						intro:'奈雪"梅你不行"主题托特包 夏日杨梅周边',
						primary_price: '119',
						slideshow:[
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye3zzn.png'
							},
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye3xRs.png'
							},
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye3vGj.png'
							}
						],
						num:'32'
					}
				],
				teacomm: [{
						pid: 1,
						img: 'https://s1.ax1x.com/2020/05/07/YeGfgA.png',
						name: '飘香茗茶系列',
						intro:'奈雪的茶 品尝悠闲·茶礼盒',
						price: '129',
						slideshow:[
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye8yWj.jpg'
							},
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye8sYQ.jpg'
							},
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye8rFg.jpg'
							},
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye80w8.jpg'
							},
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye8BTS.jpg'
							}
						],
						num:'50'
					},
					{
						pid: 2,
						img: 'https://s1.ax1x.com/2020/05/07/YeGb4g.png',
						name: '雅月·名优乌龙',
						intro:'奈雪【小茶盒】雅月·名优乌龙 上等乌龙',
						price: '59',
						slideshow:[
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye8cSs.jpg'
							},
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye8gln.jpg'
							},
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye82yq.jpg'
							},
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye8RO0.jpg'
							},
							{
								slideshow:'https://s1.ax1x.com/2020/05/07/Ye8fmV.jpg'
							}
						],
						num:'32'
					}
				],
				kefu:'https://s1.ax1x.com/2020/05/07/YeD26O.png'
			}
		},
		methods: {
			news(n){
				console.log(n)
				var news = JSON.stringify(n);
				uni.navigateTo({
					url:'../commdity_details/commdity_details?news='+ encodeURIComponent(news)
				})
			},
			tea(t){
				console.log(t)
				var news = JSON.stringify(t);
				uni.navigateTo({
					url:'../commdity_details/commdity_details?news='+ encodeURIComponent(news)
				})
			}
		}
	}
</script>

<style>
	.swiper {
		width: 100%;
		height: 900upx;
	}

	.swiperimg {
		width: 100%;
		height: 900upx;
	}

	.comm {
		width: 100%;
		height: 900upx;
		background-color: #EEF6DE;
	}

	.coupon {
		width: 90%;
		height: 220upx;
		margin: 5%;
	}

	.coupon2 {
		width: 90%;
		height: 480upx;
		margin: 10% 5%;
	}

	.new {
		width: 100%;
		height: 1000upx;
	}

	.newimg {
		width: 40%;
		height: 130upx;
		margin: 20% 0 0 30%;
	}

	.newbanner {
		width: 95%;
		height: 400upx;
		margin: 2.5%;
	}

	.newcomm {
		width: 100%;
		height: 450upx;
		margin: 2.5% 0;
		display: flex;
	}

	.newlist {
		width: 48%;
		height: 450upx;
		border: solid 2upx #BBCA91;
		border-radius: 20upx;
		margin: 0 2%;
	}

	.newlist image {
		width: 100%;
		height: 300upx;
	}

	.new_name {
		color: #686868;
		margin: 2%;
	}

	.new_price {
		font-size: 40upx;
		margin: 5% 0 0 0;
		display: flex;
		justify-content: space-between;
	}

	.teaimg {
		width: 40%;
		height: 100upx;
		margin: 50% 0 0 30%;
	}
	.service{
		position: fixed;
		bottom: 60upx;
		right: 20upx;
		z-index: 2;
		width: 80rpx;
		height: 80rpx;
		border-radius: 50%;
		background-color: white;
	}
	.serv{
		width: 80rpx;
		height: 80rpx;
		border-radius: 50%;
		margin: 1%;
	}
</style>
