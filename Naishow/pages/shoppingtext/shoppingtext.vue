<template>
	<view>
		<!-- 购物列表 html -->
		<view class="listCount">
		    <checkbox-group @change="checkboxChange">
		        <label class="listItem" v-for="item in carArr" :key="item.value">
		            <view class="checkBox">
		                <checkbox style="transform:scale(0.9)" :value="item.value" :checked="item.checked"  v-show="item.whether"/>
		                <view class="notGoods" v-show="!item.whether">
		                    无货
		                </view>
		            </view>
		            <view class="itemShow">
		                <view class="listImg">
		                    <image :src="item.src" mode="aspectFill" style="width: 100%; height: 100%;"></image>
		                </view>
		                <view class="itemCont">
		                    <view class="itemName">
		                        {{item.name}}
		                    </view>
		                    <view class="itemGrade">
		                        品相优良
		                        <text class="aliIcon">&#xe658;</text>
		                    </view>
		                    <view class="itemPriceTool">
		                        <view class="price">
		                            ￥{{item.price}}
		                        </view>
		                        <view class="itemTool">
		                            <text class="toolTwo" v-show="!item.whether">
		                                到货提醒
		                            </text>
		                            <text class="toolOne" v-show="!item.whether">
		                                预定
		                            </text>
		                            <text class="toolOne" v-show="item.whether"  @click="showBottomVisible = true">
		                                锁定
		                            </text>
		                        </view>
		                    </view>
		                    <view class="aliIcon">
		                        &#xe6a7;
		                    </view>
		                </view>
		            </view>
		        </label>
		    </checkbox-group>
		</view>
		<!-- 全选按钮 -->
		<checkbox-group @change="changeBook">
		    <label>
		        <checkbox style="transform:scale(0.9)" :checked="allFlag.checked" :value="allFlag.cb"/> 全选
		    </label>
		</checkbox-group>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				allFlag: {
				    value: 'cb',
				    checked: false
				},
				carArr: [
				    {
				        value: 'USA',
				        name: '摩根财团',
				        price: '25.22',
				        whether: true,
				        src: 'http://img3m6.ddimg.cn/56/6/28519976-1_l_3.jpg'
				    },
				    {
				        value: 'CHN',
				        name: '中国高校之殇',
				        price: '5.00',
				        whether: true,
				        src: 'http://img3m1.ddimg.cn/26/6/28510541-1_l_3.jpg'
				    },
				    {
				        value: 'BRA',
				        name: '华夏万军',
				        price: '63.09',
				        whether: true,
				        src: 'http://img3m9.ddimg.cn/22/13/28495489-1_l_9.jpg'
				    },
				    {
				        value: 'JPN',
				        name: '音乐迷醉指南',
				        price: '13.21',
				        whether: true,
				        src: 'http://img3m8.ddimg.cn/70/21/28509298-1_l_3.jpg'
				    },
				    {
				        value: 'ENG',
				        name: '纸上美术馆',
				        price: '36.35',
				        whether: true,
				        src: 'http://img3m8.ddimg.cn/4/25/28500718-1_l_2.jpg'
				    },
				    {
				        value: 'FRA',
				        name: '艺术哲学',
				        price: '14.36',
				        whether: false,
				        src: 'http://img3m8.ddimg.cn/40/9/23525608-1_l_4.jpg'
				    },
				    {
				        value: 'BRAs',
				        name: '华夏万军',
				        price: '63.09',
				        whether: false,
				        src: 'http://img3m9.ddimg.cn/22/13/28495489-1_l_9.jpg'
				    }
				]
			}
		},
		methods: {
			changeBook (e) {
			    if (e.detail.value.length == 0) {
			        this.carArr.map(item => this.$set(item, 'checked', false))
			        this.$set(this.allFlag, 'checked', false)
			    } else {
			        this.carArr.map(item => this.$set(item, 'checked', true))
			        this.$set(this.allFlag, 'checked', true)
			    }
			},
			// list checkbox
			checkboxChange (e) {
				var items = this.carArr,
					values = e.detail.value;
				for (var i = 0, lenI = items.length; i < lenI; ++i) {
					const item = items[i]
					if(values.includes(item.value)){
						this.$set(item,'checked',true)
					}else{
						this.$set(item,'checked',false)
					}
				}
				//  商品是否全部勾选，判断全选与否状态
				var offCarArr = []
				this.carArr.forEach(item => item.whether == true? offCarArr.push(item): '')
				let allChecks = offCarArr.every(item => item.checked == true)     
				allChecks ? this.$set(this.allFlag, 'checked', true) :this.$set(this.allFlag, 'checked', false)
			}
		}
	}
</script>

<style>

</style>
