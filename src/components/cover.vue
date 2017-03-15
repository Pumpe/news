<template>
	<div class="jump-cover">
		<loading></loading>
	</div>
</template>

<script>
	import Loading from './loading.vue'

	export default {
		name:'cover',
		components:{
			Loading
		}
	}
</script>

<style scoped>
	.jump-cover{
		position: fixed;
		left:0;
		top:0;
		width: 100%;
		height:100%;
		z-index: 1001;
		background: #f5f5f5;
	}
	.jump-cover .loading{
		position: absolute;
		margin:0;
		left:50%;
		top:50%;
		transform: translate3d(-50%,-50%,0);
	}
</style>