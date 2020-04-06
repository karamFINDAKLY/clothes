<template>
  <div id="app">
    
    <div class="nav-bar"></div>
        <div class="cart">
            <p>Panier({{ cart.length }})</p>
            
        </div>
       <product :premium="premium" @add-to-cart="updateCart"></product>
   </div>

</template>

<script>
import product from './components/product.vue'

export default {
  name: 'App',
     data: function () {
  return {
  premium: true,
        cart: []  }
},
    methods: {
        updateCart(id) {
            this.cart.push(id)
        }
    },
  components: {
    product
  }}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
  .nav-bar {
    background: linear-gradient(-90deg, rgb(66, 123, 146), rgb(114, 196, 243));
    height: 60px;
    margin-bottom: 15px;
  }
</style>
