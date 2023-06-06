<template>
	<view class="content">
		<navigator url="/pages/list/list">新闻列表</navigator>
		<navigator url="/pages/about/about">关于我们</navigator>
		<h1>uniapp,我来了</h1>
		<span>正常使用h5页面字体是会加粗的</span>
		<span>在微信开发者工具里面不会加粗</span>
		<icon type="success" size="25"></icon>
		<p>view是块标签 text是行内标签</p>
		<!-- //滑动效果 -->
		<scroll-view class="scroll" scroll-x>
			<view class="group" >
				<view class="item">
					111
				</view>
				<view class="item">
					222
				</view>
				<view class="item">
					333
				</view>
				<view class="item">
					444
				</view>
				<view class="item">
					555
				</view>
			</view>
		</scroll-view>
		<!-- //整块滑动效果 -->
		<swiper class="swiper"  circular autoplay="3000" duration="200">
			<swiper-item class="item">
				<image src="/static/logo.png" mode=""></image>
			</swiper-item>
			<swiper-item class="item">
				<image src="/static/logo.png" mode=""></image>
			</swiper-item>
			<swiper-item class="item">
				<image src="/static/logo.png" mode=""></image>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		
	}
</script>

<style lang="scss">
	.content {
		//rpx可适应单位 以后使用rpx
		width: 400px;
		height: 500px;
		display: flex;
		background-color: pink;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		h1{
			font-size: 40px;
			color: red;
		}
		.scroll{
			border:1rpx solid red;
			box-sizing:border-box;
			height: 220rpx;
			.group{
				white-space: nowrap;
				.item{
					width: 220rpx;
					height: 220rpx;
					background:blue;
					display: inline-block;
					margin-right: 10rpx;
				}
			}
		}
		.swiper{
			.item {
				background-color: yellow;
				width: 230rpx;
				image {
					width: 220rpx;
				}
			}
		}
	}
	
</style>
