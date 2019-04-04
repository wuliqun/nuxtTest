<template>
	<input type="color" name="" v-model="color">
</template>

<script>
	export default{
		props:['value'],
		data(){
			return{
				color:''
			}
		},
		watch:{
			color(val){
				if(val != this.value){
					this.$emit('change',val);
				}
			}
		},
		mounted(){
			this.color = this.value;
		}
	}
</script>