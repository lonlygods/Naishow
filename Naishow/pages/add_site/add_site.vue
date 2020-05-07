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
				<van-field :value="userName" required clearable label="收货人" icon="question-o" placeholder="收货人姓名"
				 @click-icon="onClickIcon" />
				<van-field :value="telNumber" label="手机号码" placeholder="收货人手机号" required border="false" />
				<view class="danyuan" @click="show = true">
					<view>省/市/区</view>
					<input type="text" placeholder="选择省/市/区" :value="carmodel" class="uni-input" />
				</view>
				<van-popup :show="show" @close="onClose" position="bottom" custom-style="height: 50%;">
					<van-area :area-list="areaList" @confirm="queren" @cancel="quxiao" />
				</van-popup>
				<van-field :value="detailInfo" label="收货地址" placeholder="请填写收货地址" required border="false" />
			</van-cell-group>
		</view>
		<van-button type="primary" size="large" color="#6CBE72" @click="add">保存并使用</van-button>
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
				// provinceName:'',
				// cityName:'',
				// countyName:'',
				detailInfo:''
			}
		},
		onLoad() {
			console.log(AreaList)
			
		},
		methods: {
			site() {
				var that = this;
				uni.chooseAddress({
					success(res) {
						console.log(res)
						that.sites = res
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
				  this.carmodel = suc.detail.values[0].name+' '+ suc.detail.values[1].name+' '+ suc.detail.values[2].name
				  this.show = false;
			  },
			  quxiao(){
				  this.show = false;
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
</style>
