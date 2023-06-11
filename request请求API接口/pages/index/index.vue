<template>
	<view class="out">
		<view class="row" v-for="item in listArr" :key="item.id" @click="clickItem(item.id)">
			<view class="title">{{item.title}}</view>
			<view class="content">{{item.body}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				listArr:[]
			}
		},
		onLoad() {
		this.getData()
		},
		methods: {
		//获取数据
		getData(){
			uni.request({
				url:"http://jsonplaceholder.typicode.com/posts",
				success:res=>{
					console.log(res);
					this.listArr=res.data
				}
			})
		},
		//跳转网页详情
		clickItem(e){
			uni.navigateTo({
				url:"/pages/detail/detail?id="+e
			})
		}
		}
	}
</script>

<style>
	.out{
		padding: 50rpx 30rpx;
	}
	.row{
		padding: 20rpx 0;
		border-bottom: 1rpx dotted #e4e4e4;
	}
	.title{
		font-size: 36rpx;
		padding-bottom: 15rpx;
		color: #22230b;
	}
	.content{
		font-size: 28rpx;
		color: #888;
	}
</style>
