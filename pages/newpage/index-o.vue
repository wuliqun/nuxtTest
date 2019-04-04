<template>
	<div class="newpage">
		<div class="left">
			<div class="side">
				<div class="tab-title">
					<div>基础组件</div>
				</div>
				<draggable @start="start" @end="end" tag="ul" class="items">
					<li class="item" v-for="item in sideData">
						<div class="img" :style="{'background':'url('+item.imgSrc+')'}">
							
						</div>
						<div class="name">
							{{item.name}}
						</div>
					</li>
				</draggable>
			</div>			
		</div>
		<div class="right">
			<div class="page-container">
				<div class="wrapper" :class="{empty:isEmpty}">
					<div v-for="item in components">
						<div v-html="item.template"></div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import draggable from 'vuedraggable'

	export default{
		data(){
			return {
				sideData:[
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'空白块'
					},
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'富文本编辑器'
					},
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'商品列表'
					},
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'动态商品'
					},
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'图片'
					},
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'拼图'
					},
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'轮播'
					},
					
				],
				components:[
					{
						type:'empty',
						template:`<div class="prevEnter">
							<div class="inner">拖拽至此</div>	
						</div>`
					}
				],
				isDragging:false
			}
		},
		methods:{
			start(){
				this.isDragging = true;
			},
			end(){
				this.isDragging = false;
			}
		},
		computed:{
			isEmpty(){
				if(!this.components.length){
					return true;
				}else{
					if(this.components.length ==1 && this.components[0].type == 'empty'){
						return true;
					}else{
						return false;
					}
				}
			}
		},
		components:{
			draggable
		},
		mounted(){//事件被阻止冒泡到document
			document.addEventListener('mousemove',(e)=>{
				if(this.isDragging){
					console.log(e);
				}
			});
		}
	}
</script>

<style lang="scss">
	*{
		margin:0;
		padding:0;
	}
	.left{
		position:absolute;
		top:10px;
		left:10px;
		bottom:10px;
		overflow-y:auto;
		width:300px;
		.side{
			background-color:#f0f0f0;
		}
		.tab-title{
			text-align:center;
			font-size:22px;
			line-height:35px;
			color:#333;
		}
		.items{
			overflow:hidden;
			margin-top:20px;
			.item{
				float:left;
				margin:10px 0 0 10px;
				list-style:none;
				width:130px;
				height:135px;
				box-sizing:border-box;
				border:2px solid #ccc;
				border-radius:10px;
				cursor:move;
				&:hover{
					border-color:#49d;
				}
			}
			.img{
				margin:15px 23px 10px;
				height:80px;
				width:80px;
				background-size:cover !important;
			}
			.name{
				text-align:center;
				font-size:14px;
				color:#49d;
			}
		}
	}
	.right{
		position:absolute;
		top:10px;
		left:320px;
		bottom:10px;
		right:10px;
		overflow-y:auto;		
	}
	.page-container{
		.wrapper{
			max-width:1200px;
			margin:0 auto;
			min-height:573px;
			border:1px dashed #ccc;
			&.empty{
				background:url(http://asset.ibanquan.com/youpage/dist/1609250000/assets/imgs/first_1.png) no-repeat center center;
			}
		}
		.prevEnter{
			height:70px;
			padding:10px;
			line-height:50px;
			text-align:center;
			background-color:rgba(68,153,221,.5);
			.inner{
				height:100%;
				outline:1px dashed #333;
			}
		}
	}
</style>