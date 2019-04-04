<template>
	<div class="img">
		<div class="img-wrapper" :style="{'background-color':value.bgColor}" :class="imgLayout">
			<img :src="value.imgSrc">
		</div>
		<div class="settings">			
			<a class="layout" @click="changeLayout">布局<span>{{value.layoutType}}</span></a>
			<div class="bg">
				<span>背景#</span>
				<div class="bgInput">
					<input type="color" name="" v-model="value.bgColor">
				</div>
			</div>
			<div class="bg">
				<span>图片链接#</span>
				<div class="bgInput">
					<input type="text" name="" v-model="value.imgSrc">
				</div>
			</div>
		</div>
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
				layoutType:1
			}
		},
		methods:{
			changeLayout(){
				this.value.layoutType ++;
				if(this.value.layoutType > 4){
					this.value.layoutType = 1;
				}
				this.$emit('input',this.value);
			}
		},
		computed:{
			imgLayout(){
				switch(this.value.layoutType){
				case 1:
					return 'ta-center';
				case 2:
					return 'ta-left';
				case 3:
					return 'ta-right';
				case 4:
					return 'cover';
				}
			}
		}
	}
</script>

<style lang="scss">
	.img{
		position:relative;
		.img-wrapper{

		}
		.ta-center{
			text-align:center;
		}
		.ta-left{
			text-align:left;
		}
		.ta-right{
			text-align:right;
		}
		.cover{
			img{
				display:block;
				width:100%;
			}
		}
		.settings{
			position:absolute;
			top:2px;
			right:50px;
			text-align:center;
			line-height:30px;
			.layout{
				float:left;
				width:80px;
				height:30px;
				cursor:pointer;
				margin-right:10px;
				border:1px solid #666;
				border-radius:4px;
				background-color:#fff;				
			}
			.bg{
				float:left;
				position:relative;
				span{
					display:block;
					width:80px;
					height:30px;
					margin-right:10px;
					cursor:pointer;	
					border-radius:4px;
					border:1px solid #666;			
					background-color:#fff;	
				}
			}
		}
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
	}
</style>
