<template>
	<view class="user">
		<div class="top">
			<image src="../../static/历史.png" mode=""></image>
			<div class="text">浏览历史</div>
		</div>
		<div class="content">
			<div class="row" v-for="item in listArr">
				<newsbox :item="item" @click.native="goDetail"></newsbox>
			</div>
		</div>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				listArr:[]
			}
		},
		onLoad(){
			this.getData()
		},
		methods:{
			//跳转到详情页
			getDetail(){
				uni.navigateTo({
					url:`/pages/detail/detail??cid=${item.classid}&id=${item.id}`
				})
			},
			//获取缓存记录
			getData(){
				let hisArr=uni.getStorageSync("historyArr")||[],
				listArr=hisArr
			}
		}
	}
</script>

<style lang="scss">
.user{
	.top {
		padding: 50rpx 0;
		background: #f8f8f8;
		color: #666;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		image{
			width: 150rpx;
			height: 150rpx;
		}
		text{
			font-size: 38rpx;
		}
	}
	.content{
		padding: 30rpx;
		.row {
			border-bottom: 1px dotted #229ddd;
			padding: 15rpx 0;
		}
	}
}
</style>
