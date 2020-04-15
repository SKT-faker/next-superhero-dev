<template>
	<view class="page">
		<swiper :indicator-dots="true" :autoplay="true" class="carousel">
			<swiper-item v-for="carousel in carouselList">
				<image 
					:src="carousel.image"
					 class="carousel"></image>
			</swiper-item>
			<!-- <swiper-item>
				<image src="../../static/carousel/spiderman.png" class="carousel"></image>
			</swiper-item> -->
		</swiper>
	</view>
</template>

<script>
	// import common from '../../common/common.js'
	
	export default {
		data() {
			return {
				carouselList: []
			}
		},
		onLoad() {
			let serverUrl = this.serverUrl;
			
			// 请求轮播图数据
			uni.request({
			    url: serverUrl + '/index/carousel/list?qq=2715705745', 
				method: "POST",
			    success: (res) => {
			        console.log(res.data);
			        
					if(res.data.status == 200){
						this.carouselList = res.data.data;
					}
			    }
			});
		},
		methods: {

		}
	}
</script>

<style>
	@import url("index.css");
</style>
