<template>
	<input type="number" name="" v-model="num">
</template>
<script>
	export default{
		props:['value'],
		data(){
			return{
				num:''
			}
		},
		watch:{
			num(val){
				if(val != this.value){
					this.$emit('change',val);
				}
			}
		},
		mounted(){
			this.num = this.value;
		}
	}
</script>