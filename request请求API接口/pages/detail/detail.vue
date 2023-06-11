<template>
	<view >
	<view class="detail">
		<view class="title">{{objData.title}}</view>
		<view class="content">{{objData.body}}</view>
	</view>
	<view class="comments">
		<view class="row" v-for="item in comments" :key="item.id">
			<view class="top">
				<view class="name">{{item.name}}</view>
				<view class="mail">{{item.email}}</view>
			</view>	
			<view class="body">
				{{item.body}}
			</view>
		</view>
	</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				objData:[],
				id:1,
				comments:[]
			};
		},
		//在onload里面接收组件之间的传智
		onLoad(e){
			this.getDetail()
			this.id=e.id
			this.getComments()
		},
		methods:{
			
			getDetail(){
				uni.showLoading({
					title:"数据加载中……"
				}),
				uni.request({
					url:"http://jsonplaceholder.typicode.com/posts/"+this.id,
					success:res=>{
						this.objData=res.data
					},
					complete:()=>{
						uni.hideLoading()
					}
				})
			},
			getComments(){
				uni.request({
					url:`http://jsonplaceholder.typicode.com/posts/${this.id}/comments`,
					success:res=>{
						this.comments=res.data
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.detail {
		padding: 30rpx;
		.title{
			font-size: 36rpx;
			color:#000;
			padding-bottom: 20rpx;
			.content{
				font-size: 30rpx;
				color:#666
			}
		}
	}
	.comments{
		padding: 30rpx;
		background-color: #f4f4f4;
		.text{
			font-size: 46rpx;
			margin-bottom: 30rpx;
		}
		.row{
			border-bottom: 1px solid #e8e8e8;
			margin-bottom: 30rpx;
			.top {
				display: flex;
				justify-content: space-between;
				font-size: 22rpx;
				color: #999;
			}
			.body {
				font-size: 28rpx;
				color:#555
			}
		}
	}
</style>
