<template>
	<view class="detail">
		<view class="title">
			{{objData.title}}
		</view>
		
		<view class="content">
			{{objData.body}}
		</view>
		
		<!-- 评论 -->
		<view class="">
			评论
		</view>
		
		
		<view class="comments">
			
			<view class="row" v-for="item in comments" :key="item.id">
				<view class="top">
					<view class="name">
						{{item.name}}
					</view>
					<view class="mail">
						{{item.email}}
					</view>
				</view>
				<view class="text">
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
				objData:{},
				id:1,
				comments:{}
			};
		
		},
		onLoad(e) {
			
			this.id=e.id
			this.getDetail();
			this.getComments();
		},
		methods:{
			// 获取详情数据
			getDetail(){
				uni.showLoading({
					title:"数据加载中",
					mask:true
				})
				uni.request({
					url:"https://jsonplaceholder.typicode.com/posts/"+this.id,
					success:res=>{
						console.log(res)
						this.objData=res.data
					},
					complete: () => {
						uni.hideLoading()
					}
				})
			},
			// 获取评论
			getComments(){
				uni.request({
					url:`https://jsonplaceholder.typicode.com/posts/${this.id}/comments`,
					success:res => {
						console.log(res)
						this.comments=res.data
					}
				})
			}
		}
		
		}
</script>

<style lang="scss">
.detail{
	.title{
		font-size: 40rpx;
		border-bottom-style: solid;
		
	}
	
	.content{
		font-size: 30rpx;
		color:grey;
	}
	.text{
		font-size: 20rpx;
		background-color: pink;
	}
	.comments{
		
		background-color: white;
		.row{
		.top{
			padding-top: 30rpx;
			display: flex;
			justify-content: space-evenly;
			
			font-size: 10rpx;
			margin-bottom: 10rpx;
			color: pink;
		}
		}	
	}
	
}
</style>
