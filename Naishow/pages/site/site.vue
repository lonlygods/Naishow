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
		<!-- <view class="sitelist">
			<van-checkbox :value="checked" checked-color="#6CBE72" @change="onChange">复选框</van-checkbox>
			<text></text>
		</view> -->
		<view class="site">
			<van-checkbox :value="checked" checked-color="#6CBE72" @change="onChange" class="check"></van-checkbox>
			<view class="site_content">
				<text>{{sites.userName}}</text>
				<text>{{sites.telNumber}}</text>
				<text>\n</text>
				<text>{{sites.provinceName}}{{sites.cityName}}{{sites.countyName}}{{sites.detailInfo}}</text>
			</view>
		</view>
		<van-button type="primary" size="large" color="#6CBE72" @click="add">保存并使用</van-button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sites:[
					{
						userName:'',
						telNumber:'',
						provinceName:'',
						cityName:'',
						countyName:'',
						detailInfo:'',
					}
				],
				checked: true
			}
		},
		onLoad() {
		},
		methods: {
			site(){
				var that = this;
				uni.chooseAddress({
				  success(res) {
				    console.log(res)
					that.sites = res
				  }
				})
			},
			onChange(event) {
			  this.checked = event.detail
			  console.log(this.sites)
			},
			add(){
				uni.navigateTo({
					url:'../add_site/add_site'
				})
			}
		}
	}
</script>

<style>
.wxsite{
	width: 100%;
	height: 100upx;
	display: flex;
	justify-content: space-between;
	background-color: #FCFCFC;
}
.wechat{
	width: 50upx;
	height: 50upx;
}
.wxleft{
	margin: 5% 0 0 5%;
}
.wxleft text{
	position: absolute;
	top: 38upx;
}
.wxright{
	margin: 5% 5% 0 0;
}
.check{
	position: absolute;
	margin: 2% 0 0 0;
}
.site {
		width: 90%;
		height: 110upx;
		border-bottom: solid 3rpx #F2F2F2;
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
</style>
