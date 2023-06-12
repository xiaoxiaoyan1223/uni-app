<template>
	<view class="home">
		<view class="scrollNav">
			<scroll-view scroll-x class="navscroll">
				<view class="item"  v-for="(item,index) in navArr"  :class="index==navIndex?'active':''" 
				@click="clickNav(index,item.id)"
				:key="item.id">{{item.classname}}</view>
			</scroll-view>
			<view class="content">
				<div class="row" v-for="item in newsArr" :key="item.id">
					<newsbox @click.native="goDetail" :item="item"></newsbox>
				</div>
			</view>
			<view class="nodata" v-if="!newsArr.length">
				<image src="../../static/logo.png" mode=""></image>
			</view>
			<view class="loading" v-if="newsArr.length">
				<view v-if="loading==1">数据加载中...</view>
				<view v-if="loading==2">没有更多了^~^</view>
			</view>
		</view> 
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navIndex:0,
				navArr:[],
				newsArr:[],
				current:1,
				loading:0
			}
		},
		onLoad() {
		this.getNavData()
		this.getNewsData()
		},
		onReachBottom(){
			if(this.loading==2){
				return
			}
			this.current++
			this.loading=1
			this.getNewsData()
		},
		methods: {
			//点击导航切换
			clickNav(index,id){
				console.log(index);
				this.navIndex=index
				this.current=1
				this.loading=0
				this.newsArr=[]
				this.getNewsData(id)
			},
			//点击跳转到详情页	
			goDetail(){
				uni.navigateTo({
					url:"/pages/detail/detail"
				})
			},
			//获取导航列表数据
			getNavData(){
				uni.request({
					url:"https://ku.qingnian8.com/dataApi/news/navlist.php",
					success:res=>{
						console.log(res);
						this.navArr=res.data
					}
				})
			},
			getNewsData(id=50){
				uni.request({
				url:"https://ku.qingnian8.com/dataApi/news/newslist.php",
				data:{
					cid:id,
					page:this.current
				},
				success:res=>{
					console.log(res);
					if(res.data.length==0){
						this.loading=2
					}
					this.newsArr=[...this.newsArr,...res.data]
				}
				})
			}
		}
	}
</script>

<style lang="scss">
	.navscroll{
		height: 100rpx;
		background-color: #F7F8FA;
		white-space: nowrap;
		//上面导航栏固定定位
		position: fixed;
		//uniapp内置css变window-top吸顶效果
		top: var(--window-top);
		z-index: 10;
		left: 0;
		//deep向内部找到滚动条 取消滚动条
		/deep/::-webkir-scrollbar{
			width: 4px !important;
			height: 1px !important;
			overflow: auto !important;
			background: transparent !important;
			-webkit-appearance:auto !important;
			display: block;
		}
		.item {
			display: inline-block;
			font-size: 40rpx;
			line-height: 100rpx;
			padding: 0 30rpx;
			color: #333;
			&.active{
				color: #229ddd;
			}
		}
	}
	.content{
		padding: 30rpx;
		padding-top: 30rpx;
		.row {
			border-bottom: 1px dotted #229ddd;
			padding: 15rpx 0;
		}
	}
	.nodata{
		display: flex;
		justify-content: center;
		image{
			width: 360rpx;
		}
	}
	.loading {
		text-align: center;
		font-size: 26rpx;
		color:#888;
		line-height: 2em;
		
	}
</style>
