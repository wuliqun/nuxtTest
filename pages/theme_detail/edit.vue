<template>
	<div>
		<div class="left">
			<div class="schema">
				<div class="schema-container">
					<div v-show="!detail">
						<div class="head">{{theme_name}}</div>
						<ul class="settings">
							<li v-for="(item,index) in schema" :class="item.type || ''">
								<a v-if="!item.type" class="setting-item" @click="showDetail(index)">{{item.name}}</a>
								<span v-if="item.type">{{item.name}}</span>
							</li>
						</ul>
					</div>
					<div v-show="detail">
						<div class="head">
						<a class="arrow" @click="back">&lt;--</a>
						{{settings.name}}</div>
						<ul class="sub-setings">
							<li v-for="(item,index) in settings.settings" class="sub-setting-item">
								<div class="sub-setting-name">{{item.title}}</div>
								<div class="option" v-for="op in item.options[0].group">
									<div v-if="op.type == 'color'">
										<input type="color" class="color" v-model="current[op.data]" />
										<div class="txt">{{op.label}}</div>
									</div>
									<div v-else-if="op.type == 'image'">
										<img :src="current[op.data]" class="img">
										<div class="operate">
											<a class="change">替换</a>
											<a class="edit">编辑</a>
										</div>
									</div>
									<div v-else-if="op.type == 'navigation'">
										
									</div>
									<div v-else-if="op.type == 'checkbox'" class="checkbox">
										<div class="txt">{{op.text}}</div>
										<input type="checkbox" :id="op.data" name="" v-model="current[op.data]"><label :for="op.data">{{op.label}}</label>
									</div>
									<div v-else-if="op.type == 'input'" class="input">
										<div class="txt">{{op.text}}</div>
										<input type="text" name="" v-model="current[op.data]">
									</div>
									<div v-else-if="op.type == 'textarea'" class="input">
										<div class="txt">{{op.text}}</div>
										<textarea type="text" name="" v-model="current[op.data]" />
									</div>
								</div>
							</li>
							<!-- 
								type:
								color
								navigator
								checkbox
								image
								link
								input
								textarea
							 -->
						</ul>
					</div>
				</div>
			</div>
		</div>
		<div class="right">
			<div class="page">
				<div class="header" :style="{'background-color':current.top_background}">
					<div class="wrapper">
						<div class="logo">
							<img src="">   
						</div>
						<ul class="navs">
							<li>
								<a href="" :style="{color:current.nav_text_color}">首页</a>
							</li>
							<li>
								<a href="" :style="{color:current.nav_text_color}">医院介绍</a>
							</li>
							<li>
								<a href="" :style="{color:current.nav_text_color}">特色科室</a>
							</li>
							<li>
								<a href="" :style="{color:current.nav_text_color}">就诊示例</a>
							</li>
							<li>
								<a href="" :style="{color:current.nav_text_color}">关于我们</a>
							</li>
						</ul>
					</div>
				</div>
				<div class="slider-container">
					<ul class="slider">
						<li class="item-1"></li>
						<li class="item-2"></li>
						<li class="item-3"></li>
					</ul>
					<div class="cursor">
						<i class="btn" :style="{'background-color':slide_index == 0 ? current.slidejs_pagination_hover : current.slidejs_pagination}"></i>
						<i class="btn" :style="{'background-color':slide_index == 1 ? current.slidejs_pagination_hover : current.slidejs_pagination}"></i>
						<i class="btn" :style="{'background-color':slide_index == 2 ? current.slidejs_pagination_hover : current.slidejs_pagination}"></i>
					</div>
				</div>
				<section class="part-1">
					<div class="wrapper">
						<ul class="skills">
							<li class="skill-item" :style="{'background-color':current.item1_bg_color}">
								<a href="">
									<p class="name">{{current.index_features_1_title}}</p>
									<p class="desc">{{current.index_features_1_content}}</p>
								</a>
							</li>
							<li class="skill-item" :style="{'background-color':current.item2_bg_color}">
								<a href="">
									<p class="name">{{current.index_features_2_title}}</p>
									<p class="desc">{{current.index_features_2_content}}</p>
								</a>
							</li>
							<li class="skill-item" :style="{'background-color':current.item3_bg_color}">
								<a href="">
									<p class="name">{{current.index_features_3_title}}</p>
									<p class="desc">{{current.index_features_3_content}}</p>
								</a>
							</li>
						</ul>
					</div>
				</section>
				<section class="part-2">
					<div class="wrapper">
						<div class="head">
							<p class="title"  :style="{'color':current['service_h_title_color']}">{{current.service_3_title}}</p>
							<p class="desc" :style="{'color':current['service_h_desc_color']}">{{current.service_3_desc}}</p>
						</div>
						<ul class="departments">
							<li>
								<div class="item-wrapper">
									<div class="img">
										<img src="">
									</div>
									<div class="info">
										<p class="name" :style="{'color':current['service-list-content_h5_color']}">{{current.service_3_list1_title}}</p>
										<p class="desc"  :style="{'color':current['service-list-content_p_color']}">{{current.service_3_list1_desc}}</p>
									</div>
								</div>
							</li>
							<li>
								<div class="item-wrapper">
									<div class="img">
										<img src="">
									</div>
									<div class="info">
										<p class="name" :style="{'color':current['service-list-content_h5_color']}">{{current.service_3_list2_title}}</p>
										<p class="desc"  :style="{'color':current['service-list-content_p_color']}">{{current.service_3_list2_desc}}</p>
									</div>
								</div>
							</li>
							<li>
								<div class="item-wrapper">
									<div class="img">
										<img src="">
									</div>
									<div class="info">
										<p class="name" :style="{'color':current['service-list-content_h5_color']}">{{current.service_3_list3_title}}</p>
										<p class="desc"  :style="{'color':current['service-list-content_p_color']}">{{current.service_3_list3_desc}}</p>
									</div>
								</div>
							</li>
							<li>
								<div class="item-wrapper">
									<div class="img">
										<img src="">
									</div>
									<div class="info">
										<p class="name" :style="{'color':current['service-list-content_h5_color']}">{{current.service_3_list4_title}}</p>
										<p class="desc"  :style="{'color':current['service-list-content_p_color']}">{{current.service_3_list4_desc}}</p>
									</div>
								</div>
							</li>
						</ul>
					</div>
				</section>
			</div>
		</div>
	</div>
</template>

<script>
	import settings from '../../data/theme-setting.json'
	import current from '../../data/current.json'
	export default{
		data(){
			return {
				schema:JSON.parse(settings),
				current:JSON.parse(current).current,
				detail:false,
				settings:null,
				theme_name:'菖蒲',
				slide_index:0
			}
		},
		methods:{
			showDetail(index){
				this.detail = true;
				this.settings = this.schema[index];
			},
			back(){
				this.detail = false;
			}
		},
		created(){
			this.settings = this.schema[0];
		}
	}
</script>
<style lang="scss">
	*{
		margin:0;
		padding:0;
		list-style:none;
	}
	.left{
		position:fixed;
		left:10px;
		top:10px;
		bottom:10px;
		width:300px;
		overflow-y:auto;	
		.schema{
			ul{
				padding:0;
			}
			li{
				list-style:none;
				border-bottom:1px solid #f5f5f5;
			}
			.head{
				overflow:hidden;
				line-height:50px;
				background-color:#333;
				text-align:center;
				font-size:16px;
				color:#fff;
			}
			.arrow{
				float:left;
				margin-left:10px;
				cursor:pointer;
			}
			.title{
				line-height:25px;
				text-indent:12px;
				background-color:#ccc;
				border-width:2px;
			}
			.setting-item{
				display:block;
				line-height:40px;
				text-indent:12px;
				&:hover{
					cursor:pointer;
					text-indent:15px;
					transiton:all .5s;
					background-color:#f1f1f1;
				}
			}
			.sub-seting-item{
				border-bottom:1px solid #ccc;
			}
			.sub-setting-name{
				font-size:16px;
				font-weight:700;
				color:#000;
				text-indent:12px;
				line-height:25px;
			}
			.option{
				overflow:hidden;
				padding:5px 0;
				&:hover{
					background-color:#f1f1f1;
				}
			}
			.color{
				padding:0;
				float:left;
				width:30px;
				height:30px;
				margin:5px 10px 0 15px;
				border-radius:50%;
				border:1px solid #000;
				&+.txt{
					line-height:40px;
				}
			}
			.img{
				float:left;
				width:120px;
				height:80px;
				margin-left:10px; 
			}
			.operate{
				margin-left:140px;
				a{
					display:block;
					color:#49d;
					cursor:pointer;
				}
			}
			.checkbox{
				overflow:hidden;
				.txt{
					float:left;
					margin-left:5px;
				}
				input{
					height:20px;
					width:20px;
					margin-left:8px;
				}
			}
			.input{
				padding-left:8px;
				input{
					height:25px;
					width:260px;
				}
				textarea{
					width:260px;
					height:80px;
				}
			}
		}
	}
	.right{
		position:fixed;
		left:315px;
		top:10px;
		bottom:10px;
		right:10px;
		overflow-y:auto;
		.header{
			overflow:hidden;
			height:70px;
			.wrapper{
				max-width:1150px;
				margin:0 auto;
			}
			.logo{
				float:left;
				height:64px;
				width:150px;
				margin:3px;
				background-color:#ff0036;
				img{
					width:100%;
					height:100%;
				}
			}
			.navs{
				float:right;
				li{
					float:left;
					line-height:70px;
					font-size:20px;
					list-style:none;
					padding:0 12px;
					margin:0 15px;
				}
			}
		}
		.slider-container{
			position:relative;	
			.slider{
				height:600px;
				li{
					position:absolute;
					list-style:none;
					top:0;
					left:0;
					width:100%;
					height:100%;
					background-color:#f0f0f0;
				}
			}
			.cursor{
				position:absolute;
				bottom:120px;
				left:0;
				width:100%;
				text-align:center;
			}
			.btn{
				display:inline-block;
				width:40px;
				height:5px;
				cursor:pointer;
			}
		}
		.part-1{
			position:relative;
			top:-100px;
			.wrapper{
				max-width:1200px;
				margin:0 auto;
			}
			.skills{
				overflow:hidden;
			}
			.skill-item{
				float:left;
				width:33%;
				height:350px;
				a{
					display:block;
					padding:130px 50px 50px;
					text-align:center;
					color:#fff;
					text-decoration:none;
				}
				.desc{
					margin-top:50px;
				}
			}
		}
		.part-2{
			.wrapper{
				max-width:1200px;
				margin:0 auto;
			}
			.head{
				text-align:center;
				.title{
					font-size:25px;
				}
			}
			.departments{
				overflow:hidden;
				margin:20px 0 0 -20px;
				li{
					float:left;
					width:25%;
					padding-left:20px;
				}
			}
			.item-wrapper{
				border:1px solid #ccc;
				border-radius:5px;
				.img{
					position:relative;
					padding-top:70%;
					img{
						position:absolute;
						top:0;
						left:0;
						width:100%;
						height:100%;
					}
				}
				.info{
					padding-left:20px;
					p{
						margin:10px 0;
					}
				}
			}
		}
	}
</style>