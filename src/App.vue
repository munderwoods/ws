<template>
  <div id="app">
    <ProductPage :products="this.products" />
  </div>
</template>

<script>
import ProductPage from './components/ProductPage.vue'
import products from './assets/products.json'

export default {
  name: 'App',
  components: {
    ProductPage
  },

  data() {
    return {
      products: products
    }
  },

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
