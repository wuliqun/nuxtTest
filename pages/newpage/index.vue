<template>
	<div class="newpage">
		<div class="left">
			<div class="side">
				<div class="tab-title">
					<div>基础组件</div>
				</div>
				<ul class="items">
					<li class="item" v-for="item in sideData" draggable="true" @dragstart="dragstart($event,item.component)">
						<div class="img" :style="{'background':'url('+item.imgSrc+')'}">							
						</div>
						<div class="name">
							{{item.name}}
						</div>
					</li>
				</ul>
			</div>			
		</div>
		<div class="right">
			<div class="page-container">
				<div class="wrapper" :class="{empty:isEmpty}" @dragover="dragenter($event)"  @dragleave="dragleave" @drop="drop">
					<div v-for="(item,index) in components" @dragover="dragenter($event,index)" class="component">
						<!-- 
							type:
								empty  拖入前位置显示
								blank  空白块
								imgContainer  图片
								richTextEditor  富文本编辑器
								slider 轮播
						 -->
						<component :is="item.type" v-model="item.options" @del="del(index)"></component>
						<assit :setting="item.setting" v-if="item.type != 'empty'" @change="change(arguments,index)" @del="del(index)"></assit>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import blank from '../../components/newpage/blank.vue'
	import empty from '../../components/newpage/empty.vue'
	import imgContainer from '../../components/newpage/img.vue'
	import richTextEditor from '../../components/newpage/richTextEditor.vue'
	import slider from '../../components/newpage/slider.vue'
	import jigsaw from '../../components/newpage/jigsaw.vue'
	import assit from '../../components/newpage/assit.vue'
	export default{
		data(){
			return {
				sideData:[
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'空白块',
						component:'blank'
					},
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'富文本编辑器',
						component:'richTextEditor'
					},
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'商品列表',
						component:'productList'
					},
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'图片',
						component:'imgContainer'
					},
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'拼图',
						component:'jigsaw'
					},
					{
						imgSrc:'//asset.ibanquan.com/image/581a3f0602282e2bcc00000a/s.png?v=1478115078',
						name:'轮播',
						component:'slider'
					},
					
				],
				components:[
				],
				hasEmpty:false,
				emptyIndex:0,
				leaveTimer:null
			}
		},
		watch:{
			// components(val){
			// 	console.log(val);
			// }
		},
		methods:{
			dragstart(e,name){
				e.dataTransfer.setData('componentName',name);
			},
			dragenter(e,index){
				e.preventDefault();
				if(this.leaveTimer){
					clearTimeout(this.leaveTimer);
				}
				if(index === undefined){//容器
					if(!this.hasEmpty){
						this.components.push({
							type:'empty'
						});
						this.hasEmpty = true;
						this.emptyIndex = this.components.length-1;
					}
				}else{//添加到现有元素前
					if(this.hasEmpty && this.emptyIndex == index -1){ //空白块在当前元素前面，不用添加
						return;
					}
					if(this.hasEmpty){
						if(index >this.emptyIndex){
							index --;
						}
						this.components.splice(this.emptyIndex,1);
					}
					this.components.splice(index,0,{
						type:'empty'
					});
					this.hasEmpty = true;
					this.emptyIndex = index;
				}			
			},
			dragleave(){
				this.leaveTimer = setTimeout(this.leave.bind(this),200);
			},
			leave(){
				if(this.hasEmpty){
					this.components.splice(this.emptyIndex,1);
					this.hasEmpty = false;
				}
			},
			drop(e){
				let name = e.dataTransfer.getData('componentName');
				let item = {};
				if(name == 'blank'){//空白块
					item.type = name;
					item.options = {
						height:80,
						bgColor:'#eeeeee',						
					}
					item.setting = [
						{
							name:'高度',
							type:'digit',
							attr:'height',
							value:'80'
						},
						{
							name:'背景颜色',
							type:'color',
							attr:'bgColor',
							value:'#eeeeee'
						}
					];
					this.components.splice(this.emptyIndex,1,item);
				}else if(name == 'imgContainer'){//图片
					item.type = name;
					item.options = {
						bgColor:'#f0f0f0',
						layoutType:1,
						imgSrc:'http://asset.ibanquan.com/image/53f649ffe2931e0b91000007/s_330x330.png',
						
					}
					item.setting = [
						{
							name:'背景颜色',
							type:'color',
							attr:'bgColor',
							value:'#f0f0f0'
						}
					];
					this.components.splice(this.emptyIndex,1,item);
				}else if(name == 'richTextEditor'){
					item.type = name;
					item.options = {
						bgColor:'#cccccc',
						html:'',
					}
					item.setting = [
						{
							name:'背景颜色',
							type:'color',
							attr:'bgColor',
							value:'#cccccc'
						}
					];
					this.components.splice(this.emptyIndex,1,item);
				}else if(name == 'slider'){
					item.type = name;
					item.options = {
						slides:[
							{
								src:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1554281837911&di=76d789927cbe09ccea7e063e2a33b4e1&imgtype=0&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F0111ee55440a300000019ae9c33662.jpg',
								link:''
							},
							{
								src:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1554281837911&di=75c2e5e0a5873b5b615ccd04f67c845f&imgtype=0&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F01b266571dd33b32f875a3996d817b.jpg%402o.jpg',
								link:''
							},

						]
					}
					this.components.splice(this.emptyIndex,1,item);
				}else if(name == 'jigsaw'){
					item.type = name;
					item.options = {
						imgSrc:new Array(9).fill(''),
						col:3,
						row:3
					}
					item.setting = [
						{
							name:'行数',
							type:'digit',
							attr:'col',
							value:3
						},
						{
							name:'列数',
							type:'digit',
							attr:'row',
							value:3
						}
					];
					this.components.splice(this.emptyIndex,1,item);
				}else{
					this.components.splice(this.emptyIndex,1);
				}				
				this.hasEmpty = false;
			},
			del(index){
				this.components.splice(index,1);
			},
			// args[0]  attr   args[1]  value
			change(args,index){
				this.components[index].options[args[0]] = args[1];
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
			blank,
			imgContainer,
			richTextEditor,
			slider,
			jigsaw,
			empty,
			assit
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
			height:100%;
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
		.component{
			position:relative;
			&:hover .assit{
				display:block;
			}
		}
		.assit{
			display:none;
		}

	}
</style>