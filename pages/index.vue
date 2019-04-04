<template>
  <section class="container">
   <navs></navs>
   <nuxt-child></nuxt-child>
  </section>
</template>

<script>
import navs from '~/components/nav'
export default {
  components:{
  	navs
  }
}
</script>

<style lang="scss">
	.container{
		margin:20px;
		
	}
</style>
