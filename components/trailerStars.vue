<template>
	<view class="movie-scroll-wapper">
		<image 
			v-for="yello in yelloScore"
			src="../static/icos/star-yellow.png"
			class="star-ico"></image>
			
		<image
			v-for="gray in grayScore"
			src="../static/icos/star-gray.png" 
			class="star-ico"></image>
		<view class="movie-score" v-if="showNum == 1">
			{{innerScore}}
		</view>
	</view>
</template>

<script>
	export default {
		name: "trailerStars",
		data() {
			return {
				yelloScore: 0,
				grayScore: 5
			};
		},
		props: {
			innerScore: 0, // 定义外部传入的分数
			showNum: 0 // 是否需要显示具体的分数 1: 显示 0: 不显示
		},
		created() {
			var tempScore = 0;
			if(this.innerScore){
				tempScore = this.innerScore;
			}
			
			var yelloScore = Number.parseInt(tempScore / 2);
			var grayScore = 5 - yelloScore;
			
			this.yelloScore = yelloScore;
			this.grayScore = grayScore;
		}
	}
</script>

<style>
.movie-scroll-wapper{
	display: flex;
	flex-direction: row;
}

.star-ico{
	width: 20rpx;
	height: 20rpx;
	margin-top: 6rpx;
}

.movie-score{
	font-size: 12px;
	color: grey;
	margin-left: 8rpx;
}
</style>
