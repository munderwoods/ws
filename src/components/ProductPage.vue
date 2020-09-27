<template>
  <div class="product-page">
		<h1>{{ this.products.name }}</h1>
		<ul class="product-list">
			<Product v-for="item in this.products.groups" :key="item.id" :product="item" />
		</ul>
  </div>
</template>

<script>
import Product from './Product'

export default {
  name: 'ProductPage',
	components: {
		Product
	},
  props: {
    products: Object
  },
}
</script>

<style scoped>
.product-list {
	display: flex;
	flex-direction: row;
	justify-content: space-around;
	flex-wrap: wrap;
}
</style>
