<template>
	<view class="content">
		<view class="uni-list">
			<view class="part2">
				<swiper class="banner-box" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
					<swiper-item v-for="(item,index) in data.top_stories" :key="index" @tap="openInfo" :data-id="item.id">
						<image class="banner-image" :src="item.image" mode="scaleToFill"></image>
					</swiper-item>
				</swiper>
			</view>
			<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in data.stories" :key="index"
			@tap="openInfo" :data-id="item.id">
				<view class="uni-media-list">
					<image class="uni-media-list-logo" :src="item.images[0]"></image>
					<view class="uni-media-list-body">
						<view class="uni-media-list-text-top">{{item.title}}</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				data: {}
			};
		},
		onLoad:function(){
			uni.request({
				url: 'https://news-at.zhihu.com/api/4/news/latest',
				method: 'GET',
				data: {},
				success: res => {
					console.log(res);
					this.data = res.data;
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			openInfo(e) {
				var id = e.currentTarget.dataset.id;
				uni.navigateTo({
					url: '../info/info?id='+id
				});
			}
		},
	}
</script>

<style>
	.content{
		text-align: center;
	}
	.uni-media-list-body{
		height: auto;
	}
	.uni-media-list-text-top{
		line-height: 1.6em;
	}
	.part2 {
		width: 100%;
		height: 360px;
		border-bottom: 20px solid #f9f9f9;
		overflow: hidden;
		position: relative;
	}
	.part2:after {
		content: " ";
		height: 20px;
		border-radius: 50%;
		background: #f9f9f9;
		position: absolute;
		bottom: -10px;
		left: -20px;
		right: -20px;
	}
	.banner-box {
		width: 100%;
		height: 100%;
	}
	.banner-image {
		width: 100%;
		height: 100%;
	}
</style>