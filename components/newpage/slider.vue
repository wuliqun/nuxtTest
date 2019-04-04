<template>
	<div class="slider">
		<div class="slider-container">
			<ul class="cursor">
				<li class="slider-item" v-for="(item,index) in value.slides" :class="{active:activeIndex == index}">
					<a :href="item.link">
						<img :src="item.src">
					</a>
				</li>
			</ul>
		</div>
		<div class="slider-cursor">
			<ul class="cursor">
				<li class="btn" v-for="n in value.slides.length" :class="{active:activeIndex == n-1}" @click="go(n-1)">{{n}}</li>
			</ul>
		</div>
		<div class="setting">
			<a class="btn" @click="showSubSetting">设置图片</a>
			<div class="sub-setting" v-show="subSetting">
				<div class="sub-left">
					<ul class="imgs">
						<li v-for="(item,index) in value.slides">
							<div class="order">图片{{index+1}}</div>
							<div class="img-sm">
								<img :src="item.src">
							</div>
							<a class="del" @click="delImg(index)">删除</a>
						</li>
					</ul>
				</div>
				<div class="sub-right">
					<div class="title">添加图片</div>
					<div class="input">
						<p><label>图片地址：</label><input type="text" name="" v-model="newImg"></p>
						<p><label>跳转链接：</label><input type="text" name="" v-model="newLink"></p>
					</div>
					<div>
						<a class="submit" @click="submit">确定</a>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return {
				activeIndex:0,
				subSetting:false,
				newImg:'',
				newLink:'',
				timer:null
			}
		},
		watch:{
			value(val){
				this.$emit('input',val);
			}
		},
		props:{
			value:{
				default:''
			}
		},
		methods:{
			delImg(index){
				this.value.slides.splice(index,1);
			},
			showSubSetting(){
				this.subSetting = true;
				this.pause();
			},
			submit(){
				this.subSetting = false;
				if(this.newImg){
					this.value.slides.push({
						src:this.newImg,
						link:this.newLink
					})
				}
				this.newLink = '';
				this.newImg = '';
				this.restart();
			},
			play(){
				if(this.timer){
					clearInterval(this.timer);
				}
				this.timer = setInterval(this.next.bind(this),5000);
			},
			pause(){
				if(this.timer){
					clearInterval(this.timer);
				}
			},
			restart(){
				this.currentIndex = 0;
				this.play()
			},
			next(){
				let index = this.activeIndex + 1;
				if(index >= this.value.slides.length){
					index = 0;
				}
				this.activeIndex = index;
				
			},
			go(index){
				this.activeIndex = index;
			}
		},
		mounted(){
			this.play();
		}
	}	
</script>

<style lang="scss">
	*{
		padding:0;
		margin:0;
		list-style:none;
	}
	.slider{
		position:relative;
		outline:1px dashed #49d;
		.slider-container{
			position:relative;
			width:100%;
			padding-top:42%;
			ul{
				position:absolute;
				top:0;
				left:0;
				width:100%;
				height:100%;
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
		.slider-item{
			position:absolute;
			opacity:0;
			top:0;
			left:0;
			width:100%;
			height:100%;
			transition:all .5s;
			&.active{
				opacity:1;
			}
			a{
				display:block;
				width:100%;
				height:100%;
			}
			img{
				width:100%;
				height:100%;
			}
		}
		.slider-cursor{
			position:absolute;
			height:20px;
			bottom:50px;
			left:0;
			right:0;
			text-align:center;
			li{
				display:inline-block;
				width:20px;
				height:20px;
				border-radius:50%;
				margin-right:22px;
				cursor:pointer;
				background-color:#ccc;
				&.active{
					background-color:#ff0036;
				}
			}
		}
		.setting{
			position:absolute;
			top:5px;
			left:10px;
			.btn{
				float:left;
				padding:0 12px;
				line-height:30px;
				background-color:#49d;
				border-radius:5px;
				cursor:pointer;
			}
		}
		.sub-setting{
			position:absolute;
			top:32px;
			left:0;	
			background-color:#f0f0f0;	
		}
		.sub-left{
			float:left;
			li{
				overflow:hidden;
				width:260px;
				height:50px;
				margin:10px 0;
				line-height:50px;

			}
			.order{
				float:left;
				margin:0 10px;
				font-size:20px;			
			}
			.img-sm{
				float:left;
				width:100px;
				height:50px;
				margin-right:12px;
				img{
					width:100%;
					height:100%;
				}
			}
			.del{
				float:left;
				cursor:pointer;
				color:#3194d0;
			}
		}
		.sub-right{
			margin-left:270px;
			width:300px;
			.title{
				margin-bottom:20px;
			}
			.input{
				input{
					width:240px;
				}
			}
			.submit{
				display:inline-block;
				margin:10px 0;
				padding:0 15px;
				line-height:30px;
				background-color:#49d;
				cursor:pointer;
			}

		}
	}
</style>