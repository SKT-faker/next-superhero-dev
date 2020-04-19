<template>
	<view class="page">
		<!-- 轮播图 start-->
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
		<!-- 轮播图 end-->
		
		<!-- 热门超英 start -->
		<view class="page-block super-hot">
			<view class="hot-title-wapper">
				<image src="../../static/icos/hot.png" class="hot-ico"></image>
				<view class="hot-title">
					热门超英
				</view>
			</view>
		</view>
		
		<scroll-view scroll-x="true" class="page-block hot">
			<view class="single-poster" v-for="superhero in hotSuperheroList" :key="superhero.id">
				<view class="poster-wapper">
					<image :src="superhero.cover" class="poster"></image>
					<view class="movie-name">
						{{superhero.name}}
					</view>
				</view>
				<trailer-stars :innerScore="superhero.score" showNum="1"></trailer-stars>
			</view>
		</scroll-view>
		
		<!-- 热门预告 start -->
		<view class="page-block super-hot">
			<view class="hot-title-wapper">
				<image src="../../static/icos/interest.png" class="hot-ico"></image>
				<view class="hot-title">
					热门预告
				</view>
			</view>
		</view>
		
		<view class="hot-movies page-block">
			<video
				v-for="trailer in hotTrailerList"
				:src="trailer.trailer"
				:poster="trailer.poster"
				class="hot-movie-single"
				controls="true"></video>
		</view>
		<!-- 热门预告 end -->
		
		<!-- 猜你喜欢 start -->
		<view class="page-block super-hot">
			<view class="hot-title-wapper">
				<image src="../../static/icos/guess-u-like.png" class="hot-ico"></image>
				<view class="hot-title">
					猜你喜欢
				</view>
			</view>
		</view>
		
		<view class="page-block guess-u-like">
			<view class="single-like-movie">
				<image :src="superhero.cover" class="poster"></image>
				<view class="movie-desc">
					<view class="movie-title">
						
					</view>
					<trailer-stars innerScore="9.1" showNum="0"></trailer-stars>
					<view></view>
				</view>
				<view class="movie-oper"></view>
			</view>
		</view>
		<!-- 猜你喜欢 end -->
	</view>
</template>

<script>
	// import common from '../../common/common.js'
	import trailerStars from '../../components/trailerStars.vue'
	
	export default {
		data() {
			return {
				carouselList: [],
				hotSuperheroList: [],
				hotTrailerList: []
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
			
			// 查询热门超英
			uni.request({
			    url: serverUrl + '/index/movie/hot?type=superhero&qq=2715705745', 
				method: "POST",
			    success: (res) => {
			        console.log(res.data);
			        
					if(res.data.status == 200){
						this.hotSuperheroList = res.data.data;
					}
			    }
			});
			
			// 查询热门预告
			uni.request({
			    url: serverUrl + '/index/movie/hot?type=trailer&qq=2715705745', 
				method: "POST",
			    success: (res) => {
			        console.log(res.data);
			        
					if(res.data.status == 200){
						this.hotTrailerList = res.data.data;
					}
			    }
			});
		},
		methods: {

		},
		components: {
			trailerStars
		}
	}
</script>

<style>
	@import url("index.css");
</style>
