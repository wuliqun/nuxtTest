<template>
	<div class="pagenew">
		<div class="header">
			<h2 class="title">页面管理</h2>
			<nuxt-link to="/newpage" class="new-btn">新增页面</nuxt-link>
		</div>
	</div>
</template>

<style lang="scss">
	.pagenew{
		.header{
			overflow:hidden;
			height:50px;
		}
		.title{
			float:left;
			line-height:50px;
			margin-left:15px;
			font-size:25px;
			font-weight:700;
		}
		.new-btn{
			float:left;
			line-height:30px;
			margin:10px 0 0 10px;
			padding:0 12px;
			background-color:#6b5;
			color:#fff;
			text-decoration:none;
		}
	}
</style>