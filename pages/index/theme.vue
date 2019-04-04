<template>
	<section class="theme">
		<div class="using">
			<div class="title">
				<h3>使用中的主题</h3>
			</div>
			<div class="theme-item">
				<p class="name">月见</p>
				<div class="content">
					<div class="btns">
						<nuxt-link to="/theme_detail/edit?id=1">主题设置</nuxt-link>
						<nuxt-link to="/theme_detail?id=1">查看</nuxt-link>
					</div>
					<div class="img">
						<nuxt-link to="/theme_detail?id=1">
							<img src="">
						</nuxt-link>
					</div>
				</div>
			</div>
		</div>
	</section>
</template>

<script>
	export default{

	}
</script>

<style lang="scss">
	.theme{
		width:500px;
		margin:50px 150px;
		.title{
			padding:12px 0 12px 20px;
			font-size:20px;
			font-weight:700;
			line-height:32px;
		}
		.theme-item{
			border:1px solid #ccc;
			border-radius:5px;
		}
		.content{
			position:relative;
		}
		.name{
			line-height:35px;
			text-indent:20px;
			font-size:14px;
			background-color:#f2f7fb;
			border-bottom:1px solid #ccc;
		}
		.btns{
			overflow:hidden;
			padding:40px 20px;
			line-height:25px;
			a{
				float:left;
				padding:0 12px;
				margin-right:10px;
				background-color:#6b5;
				color:#fff;
				text-decoration:none;
			}
		}
		.img{
			position:absolute;
			width:90px;
			height:120px;
			background-color:#ff0036;
			top:-30px;
			right:20px;
			a{
				display:block;
				height:100%;
			}
			img{
				height:100%;
				width:100%;
			}
		}
	}
</style>