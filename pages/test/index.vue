<template>
	<div id="container" @dragover="move" @drop="drop">
		<div class="block" :style="{top:y + 'px',left:x + 'px'}" draggable="true" @dragstart="dragStart"></div>
	</div>
</template>

<script>
	export default{
		data(){
			return {
				x:0,
				y:0,
				xEdge:0, //top的最大边界
				yEdge:0,  //left的最大边界,
				isDragging:false,
				eventX:0,
				eventY:0
			}
		},
		methods:{
			dragStart(e){
				this.eventX = e.clientX;
				this.eventY = e.clientY;
			},
			drop(){
			},
			move(e){
				let x = e.clientX;
				let y = e.clientY;
				this.x = Math.max(Math.min(this.xEdge,this.x + x - this.eventX),0);
				this.y = Math.max(Math.min(this.yEdge,this.y + y - this.eventY),0);
				this.eventX = x;
				this.eventY = y;
			}
		},
		// 计算最大边界
		mounted(){
			let c = document.querySelector('#container');
			let b = c.querySelector('.block');
			this.yEdge = c.offsetHeight - b.offsetHeight;
			this.xEdge = c.offsetWidth - b.offsetWidth;
			// console.log(this.xEdge,'---',this.yEdge);
		}
	}
</script>

<style lang="scss">
	#container{
		position:relative;
		height:500px;
		background-color:#f0f0f0;
		.block{
			position:absolute;
			width:300px;
			height:100px;
			background-color:#ff0036;
			cursor:move;
		}
	}
</style>