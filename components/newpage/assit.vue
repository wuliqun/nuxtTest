<!-- 新建页面组件的操作图标，以及组件的全局设置 -->
<template>
	<div class="assit">
		<div>
			<a class="icon del" @click="$emit('del')"></a>
		</div>
		<div>
			<a class="icon drag"></a>
		</div>
		<div v-if="setting" class="setting-container">
			<a class="icon setting"></a>
			<div class="setting-panel">
				<div v-for="(item,index) in setting">
					<div class="title">{{item.name}}</div>
					<!-- 使用arguments接受子组件传来的参数，同时也能传入自定义参数 -->
					<component :is="item.type" :value="item.value" @change="change(arguments,index)"></component>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	//props：setting
	// 格式 [ ]  
	// {name:'',type:'',value:'',attr:''对应属性名}
	import color from './color-picker.vue'
	import digit from './digit-input.vue'
	export default{
		data(){
			return {}
		},
		props:['setting'],
		methods:{
			change(args,index){
				this.$emit('change',this.setting[index].attr,args[0]);
			}
		},
		components:{
			color,
			digit
		}
	}
</script>

<style lang="scss" scoped>
	.assit{
		position:absolute;
		top:1px;
		right:1px;
		width:40px;
		.icon{
			display:block;
			height:40px;
			background-color:#ccc;
			&:hover{
				background-color:#49d;
			}
		}
		.setting-container{
			position:relative;
		}
		.setting-panel{
			position:absolute;
			top:0;
			left:-308px;
			width:288px;
		}
	}
</style>