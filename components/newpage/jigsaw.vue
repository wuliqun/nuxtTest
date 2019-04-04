<template>
	<div class="jigsaw">
		<ul class="container">
			<li v-for="n in value.col*value.row" :style="{width:width}" class="img">
				<div>
					<img :src="value.imgSrc[n-1]" v-show="value.imgSrc[n-1]">
					<div class="edit">
						<p>修改图片链接</p>
						<p>链接：<input type="text" v-model="value.imgSrc[n-1]" name=""></p>
					</div>
				</div>
			</li>
		</ul>	
	</div>
</template>

<script>
	export default{
		props:{
			value:{
				default:''
			}
		},
		watch:{
			value(val){
				this.$emit('input',val);
			}
		},
		data(){
			return {
				setting:false,
				col:0,
				row:0
			}
		},
		methods:{
			showSetting(){
				this.setting = true;
			},
			change(){
				this.setting = false;
				this.col = parseInt(this.col) || 0;
				this.row = parseInt(this.row) || 0;
				if(this.col && this.row){
					this.value.col = this.col;
					this.value.row = this.row;
					this.value.imgSrc.splice(this.row*this.col);
				}
			}
		},
		computed:{
			width(){
				return (1/this.value.col*100).toFixed(2) + '%';
			}
		},
		mounted(){
			this.col = this.value.col;
			this.row = this.value.row;
		}
	}
</script>

<style lang="scss">
	.jigsaw{
		position:relative;
		.operate{
			position:absolute;
			top:3px;
			right:3px;
			width:40px;
			.op{
				display:block;
				height:30px;
				margin-bottom:2px;
				cursor:pointer;
				&:hover{
					background-color:#49d;
				}
			}
		}
		.setting{
			position:relative;
		}
		.sub-setting{
			display:none;
			position:absolute;
			top:-20px;
			left:-100px;
		}
		.container{
			overflow:hidden;
		}
		.img{
			float:left;
			position:relative;
			div{
				padding-bottom:100%;
			}
			img{
				position:absolute;
				height:100%;
				width:100%;
			}
			.edit{
				position:absolute;
				display:none;
			}
			&:hover{
				background:#ccc;
				.edit{
					display:block;
				}
			}
		}
		.panel{
			position:absolute;
			left:-100px;
			top:32px;
			width:200px;
			background-color:#fff;
			border:1px solid #ccc;
			.btn{
				width:50px;
				line-height:28px;
				margin:11px;
				text-align:center;
				background-color:#49d;

			}
		}
	}
</style>