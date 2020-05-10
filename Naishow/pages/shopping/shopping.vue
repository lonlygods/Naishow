<template>
	<view class="big">
		<view class="headhome">
			<view class="homeleft" @click="home">
				<van-icon name="shop-o" color="#5D5D5E" size="20px" />
				<text>奈雪の茶</text>
				<van-icon name="arrow" color="#9B9C9E" size="16px" />
			</view>
			<view class="homeright">
				<text>编辑</text>
			</view>
		</view>

		<view class="commditylist" v-for="(c,index) in commdity" :key="index">
			<van-swipe-cell right-width="65">
				<view class="msg">
					<van-checkbox :value="c.check" checked-color="#6CBE72" @change="radio" :data-index="index" class="check"></van-checkbox>
					<view class="msg1">
						<image :src="c.img" class="msgbig"></image>
					</view>
					<view class="right2">
						<text class="msgsize">{{c.intro}}</text>
						<view class="price_num">
							<text style="color: #6CBE72;font-weight: bold;">￥{{c.price}}.0</text>
							<van-stepper :value="c.step" :data-index="index" :min="red" max="10" @change="onstep" @overlimit="reduce" />
						</view>
					</view>
				</view>
				<view slot="right" class="van-swipe-cell__right" @click="delcomm(index)">删除</view>
			</van-swipe-cell>
		</view>


		<view class="bon">
			<van-submit-bar :price="total" button-text="结算" @submit="onClickButton" :tip="true">
				<van-checkbox :value="checked" checked-color="#6CBE72" @change="onChange" class="checkde">全选</van-checkbox>
			</van-submit-bar>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				checked: true,
				commdity: [],
				popupimg: '',
				step: '',
				total: '',
				red: 1,
				totalnum:''
			}
		},
		onLoad() {

		},
		onShow() {
			var commlist = uni.getStorageSync('commlist');
			console.log(commlist);
			this.commdity = commlist;
			console.log(this.commdity);
			this.totall();
		},
		methods: {
			home() {
				uni.switchTab({
					url: '../index/index'
				})
			},

			onClickButton() {
				console.log('结算')
			},
			onstep(event) {
				this.step = event.detail;
				this.commdity[event.currentTarget.dataset.index].step = event.detail;
				this.stepss();
			},

			//步进器减
			reduce() {
				console.log(1)
				if (this.red <= 1) {
					uni.showToast({
						title: '该商品1件起售哦',
						duration: 2000
					})
				}
			},
			//单选
			radio(rea) {
				this.commdity[rea.currentTarget.dataset.index].check = !this.commdity[rea.currentTarget.dataset.index].check;
				for (let i in this.commdity) {
					if (this.commdity[i].check === true) {
						this.checked = true
					} else {
						this.checked = false
						break
					}
				}
				this.stepss();
			},
			//全选
			onChange() {
				this.checked = !this.checked
				var total = 0;
				for (let i in this.commdity) {
					if (this.checked == true) {
						this.commdity[i].check = true
					} else {
						this.commdity[i].check = false
					}
					total += (this.commdity[i].price * this.commdity[i].step) * 100
					if (this.checked == true) {
						this.total = total;
					} else {
						this.total = 0;
					}
				}
				this.totall();
			},
			//单选按钮与步进器公共函数
			stepss() {
				var total = 0;
				var totalnum = 0;
				for (let c in this.commdity) {
					if (this.commdity[c].check == true) {
						total += (this.commdity[c].price * this.commdity[c].step) * 100
					}
					totalnum += Number(this.commdity[c].step)
				}
				this.total = total;
				this.totalnum = totalnum;
				console.log('总数量：'+this.totalnum)
				uni.setStorageSync('totalnum',this.totalnum)
			},
			//全选按钮与onshow公共函数
			totall() {
				var total = 0;
				var totalnum = 0;
				for (let c in this.commdity) {
					if (this.checked == true) {
						this.commdity[c].check = true
					} else {
						this.commdity[c].check = false
					}
					if (this.commdity[c].check == true) {
						total += (this.commdity[c].price * this.commdity[c].step) * 100
					}
					totalnum += Number(this.commdity[c].step)
				}
				this.totalnum = totalnum;
				console.log('总数量：'+this.totalnum);
				uni.setStorageSync('totalnum',this.totalnum)
				// console.log(total)
				if (this.checked == true) {
					this.total = total;
				} else {
					this.total = 0;
				}
			},
			//删除商品
			delcomm(index){
				var commlist =this.commdity;
				commlist.splice(index,1)
				this.stepss();
				uni.setStorageSync('commlist',commlist);
			}
		}
	}
</script>

<style>
	.big {
		width: 100%;
		height: 1400upx;
		background-color: #F9F9F9;
		position: absolute;
		top: 0;
	}

	.headhome {
		width: 100%;
		height: 80upx;
		background-color: #FFFFFF;
		display: flex;
		justify-content: space-between;
		line-height: 80upx;
	}

	.homeleft {
		margin: 0 0 0 3%;
	}

	.homeright {
		margin: 0 3% 0 0;
	}

	.commditylist {
		width: 95%;
		height: 240upx;
		background-color: #FFFFFF;
		border-radius: 10upx;
		margin: 3% 2.5%;
	}

	.bon button {
		color: #FFFFFF;
		background-color: #69C248;
		border-radius: 40upx;
		font-weight: bold;
		border: 0;
		height: 80upx;
	}

	.bon price {
		color: #69C248;
		font-weight: bold;
	}

	.title {
		display: flex;
		color: #5D5D5E;
		font-size: 36upx;
		margin: 5%;
	}

	.msg {
		width: 100%;
		height: 240upx;
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

	.van-swipe-cell__right {
		display: inline-block;
		width: 65px;
		height: 44px;
		font-size: 15px;
		line-height: 130px;
		color: #fff;
		text-align: center;
		font-weight: bold;
		background-color: #f44;
	}
	.check{
		margin: 12% 2%;
	}
	.checkde{
		margin: 0 4%;
	}
</style>
