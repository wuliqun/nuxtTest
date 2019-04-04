<template>
	<div class="blank" :style="{height:value.height+'px','background-color':value.bgColor}"  :class="{active:showSetting}">
		<div class="inner" :style="{'line-height':value.height + 'px'}">
			空白块 实际高度：{{value.height}}px
		</div>
<!-- 		<div class="operate">
			<a class="op" @click="$emit('del')">删除</a>
			<a class="op">移动</a>
			<div class="op setting" @click.stop="toggleSetting">
				<span>设置</span>
				<div class="sub-setting" @click.stop>
					<input type="number" name="" min="20" v-model="height">
					<input type="color" name="" v-model="bgColor">
				</div>
			</div>
		</div> -->
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
			showSetting(val){
				if(!val){
					let height = parseInt(this.height) || 20;
					if(height < 20){
						height = 20;
					}
					this.value.height = height;
					this.value.bgColor = this.bgColor;
					this.$emit('input',this.value);
				}
			}
		},
		data(){
			return{
				showSetting:false,
				height:0,
				bgColor:''
			}
		},
		methods:{
			toggleSetting(){
				this.showSetting = !this.showSetting;
			},
			dragstart(e){

			}
		},
		mounted(){
			document.addEventListener('click',()=>{
				this.showSetting = false;
			});
			this.height = this.value.height;
			this.bgColor = this.value.bgColor;
		}
	}
</script>
<style lang="scss">
	.blank{
		position:relative;
		padding:7px;
		border:3px solid;
		box-sizing:content-box;
		border-color:transparent;	
		.inner{
			display:none;
			outline:1px dashed #333;
			text-align:center;
		}
		&:hover{
			border-color:#49d;
			.inner{
				display:block;
			}
			.operate{
				display:block;
			}
		}
		&.active{
			border-color:#49d;
			.operate{
				display:block;
			}
			.setting{
				background-color:#49d;
			}
			.sub-setting{
				display:block;
			}
		}
		// .operate{
		// 	display:none;
		// 	position:absolute;
		// 	top:3px;
		// 	right:3px;
		// 	width:40px;
		// 	.op{
		// 		display:block;
		// 		height:30px;
		// 		margin-bottom:2px;
		// 		cursor:pointer;
		// 		&:hover{
		// 			background-color:#49d;
		// 		}
		// 	}
		// }
		// .setting{
		// 	position:relative;
		// }
		// .sub-setting{
		// 	display:none;
		// 	position:absolute;
		// 	top:-20px;
		// 	left:-100px;
		// }
	}
</style>