<template>
	<view class="show" >
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
			this.getDate();
		},
		methods: {
			// 获取网络数据
			
			getDate(){
				uni.request({
					url:"https://jsonplaceholder.typicode.com/posts",
					success:res=>{
						console.log(res)
						this.listArr=res.data
					}
				})
			},
			
			// 点击跳转详情
			clickItem(e){
				
				uni.navigateTo({
					url:"/pages/detail/detail?id="+e
				})
			}
		}
	}
</script>

<style>
.show{
	
 .row{
	 
            display: flex;
            flex-direction: column;
            flex-wrap: wrap;
            /* 需要指定高度 */
            height: 200px;
			
			
			
			margin-top: 20rpx;
			.title{
				background-color: wheat;
				
			}
			
			.content{
				font-size: 10rpx;
			}
        }
		
		}
</style>
