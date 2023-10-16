<template>
  <div id="app">
    <SearchProduct></SearchProduct>
  </div>
</template>

<script>
import SearchProduct from './components/SearchProduct.vue'

export default {
  name: 'App',
  components: {
    SearchProduct
  }
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
