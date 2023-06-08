<template>
	<view class="content">
		<image class="logo" src="/static/logo.png" @click="clickImg"></image>
		<view class="text-area">
			<text class="title" @click="clickBox">{{title}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				arr:["红楼梦","三国演义","水浒传","西游记"]
			}
		},
		onLoad() {
			uni.showLoading({
				title:"数据加载中……",
				//加载的时候是不可以点击其他的地方的
				mask:"true"
			})
			setTimeout(()=>{
				uni.hideLoading()
			},2000)
		},
		methods: {
			clickImg(){
				uni.showToast({
					title:"发布失败",
					icon:"error",
					mask:true
					
				})
			},
			// clickBox(){
			// 	uni.showModal({
			// 		title:"手机验证",
			// 		editable:true,
			// 		placeholderText:"请输入手机号"
					
			// 	})
			// }
			clickBox(){
				// uni.showModal({
				// 	title:"手机验证",
				// 	success:res=>{
				// 		if(res.confirm){
				// 			uni.navigateTo({
				// 				url:"pages/about/about"
				// 			})
				// 		}
				// 	},
				// 	fail:err=>{
				// 		uni.showToast({
				// 			title:"取消"
				// 		})
				// 	}
					
				// })
				//类似picker
				uni.showActionSheet({
					itemList:this.arr,
					success:res=>{
						console.log(this.arr[res.tapIndex]);
					}
				})
			}

		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
