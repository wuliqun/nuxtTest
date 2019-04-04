<template>
	<div class="richText">
		<div class="text" v-html="value.html" :style="{'background-color':value.bgColor}"></div>
		<div class="settings">
			<div class="bg">
				<span>背景#</span>
				<div class="bgInput">
					<input type="color" name="" v-model="value.bgColor">
				</div>
			</div>
		</div>
		<div class="editor" v-show="showEditor">
			<div class="close" @click="hideEditor">关闭</div>
			<div class="editor-wrapper">
				<div class="quill-editor" 
			       v-model="value.html"
			       v-quill:myQuillEditor="editorOption">
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
			return{
				showEditor:false,
				editorOption:{}
			}
		},
		methods:{
			show(){
				this.showEditor = true;
			},
			hideEditor(){
				this.showEditor = false;
			}
		}
	}
</script>

<style lang="scss">
	.richText{
		position:relative;
		.text{
			height:400px;
		}	
		.settings{
			position:absolute;
			top:2px;
			right:50px;
			text-align:center;
			line-height:30px;
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
		.editor{
			position:absolute;
			top:0;
			left:0;
			width:100%;
			padding:20px;
			background-color:rgba(230,230,230,.5);
		}
		.editor-wrapper{
			width:800px;
			background-color:#fff;
			.quill-editor{
				height:350px;
			}
		}
		.close{
			width:80px;
			height:30px;
			line-height:30px;
			text-align:center;
			background-color:#49d;
			border-radius:10px;
			margin:10px;
			cursor:pointer;
		}
	}
</style>