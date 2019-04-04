<template>
	<div class="nav">
		<nuxt-link to="/">首页</nuxt-link>
	   	 <nuxt-link to="theme">主题风格</nuxt-link>
	     <nuxt-link to="pagenew">自定义页面</nuxt-link>
	</div>
</template>

<script>
	export default{
		data(){
			return {}
		}
	}
</script>

<style lang="scss">
	.nav{
		text-align:center;
		a{
			display:inline-block;
			padding:12px;
			line-height:30px;
			text-decoration:none;
			background-color:#ccc;
			font-size:16px;
			color:#000;
			&:hover{
				background-color:#41b883;
			}
			&.nuxt-link-active{
				background-color:#41b883;
			}
		}
	}
</style>
