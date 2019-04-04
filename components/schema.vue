<template>
				<div class="schema">
					<div class="schema-container">
						<div v-show="!detail">
							<div class="head">菖蒲</div>
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
									<div class="option" v-for="op in item.options.group">
										<div v-if="op.type==='color'">
											<div class="color" :style="{'background-color':}"></div>
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
</template>
<script>
		export default{
		data(){
			return {
				detail:false,
				settings:null
			}
		},
		props:['schema'],
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
	}
</style>