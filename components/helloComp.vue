<template> <!-- 定义组件的名称为helloComp -->
	<view>
		{{msg}}
		<view>
			<input type="text" :value="myval" class="txt"/>
		</view>
	</view>
</template>

<script>
	export default {
		name: "helloComp",
		data() {
			return {
				msg: "你好，这是自定义组件~~~"
			};
		},
		props:{
			myval: {
				type: String
			}
		}
	}
</script>

<style>
.txt{
	color: red;
}
</style>
