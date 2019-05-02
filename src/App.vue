<template>
  <div id="app">
    <div class="nav-bar"></div>
    <div class="product">
      <div class="product-image">
        <img :src="image">
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p>{{ description }}</p>
        <a :href="link">Visit</a>
        <p v-if="inventory > 10">In stock</p>
        <p v-else-if="inventory <= 10 && inventory >0">Almost sold out!</p>
        <p v-if="inventory === 0">Out of stock</p>
        <ul>
          <li :key="detail" v-for="detail in details">{{detail}}</li>
        </ul>
        <div :key='variant' v-for="variant in variants">
          <p @mouseover="updateProduct(variant.variantImage)">{{variant.variantColor}}</p>
        </div>
        <button v-on:click="addToCart">Add to cart</button>
        <div class="cart">
          <p>Cart({{cart}})</p>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
  import HelloWorld from './components/HelloWorld.vue'

  export default {
    name: 'app',
    data() {
      return {
        product: "socks",
        description: "these guys feel really comfortable",
        image: require('./assets/vmSocks-green.jpg'),
        link: "https://heybuddy",
        inventory: 3,
        details: ['80% cotton', '20% polyester', 'Gender-neutral'],
        variants: [
          {
            variantId: 2234,
            variantColor: 'green',
            variantImage: require('./assets/vmSocks-green.jpg')
          },
          {
            variantId: 2235,
            variantColor: 'blue',
            variantImage: require('./assets/vmSocks-blue.jpg')

          }
        ],
        cart: 0
      }
    },
    methods: {
      addToCart: function() {
        this.cart++
      },
      updateProduct: function(variantImage)  {this.image = variantImage}
    },
    components: {
      HelloWorld
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 60px;
    margin: 0px;
    padding: 0px
  }

  body {
    font-family: tahoma;
    color: #282828;
    margin: 0px;
  }

  .nav-bar {
    background: linear-gradient(-90deg, #84CF6A, #16C0B0);
    height: 60px;
    margin-bottom: 15px;
  }

  .product {
    display: flex;
    flex-flow: wrap;
    padding: 1rem;
  }

  img {
    border: 1px solid #d8d8d8;
    width: 70%;
    margin: 40px;
    box-shadow: 0px .5px 1px #d8d8d8;
  }

  .product-image {
    width: 80%;
  }

  .product-image,
  .product-info {
    margin-top: 10px;
    width: 50%;
  }

  .color-box {
    width: 40px;
    height: 40px;
    margin-top: 5px;
  }

  .cart {
    margin-right: 25px;
    float: right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
  }

  button {
    margin-top: 30px;
    border: none;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
  }

  .disabledButton {
    background-color: #d8d8d8;
  }

  .review-form {
    width: 400px;
    padding: 20px;
    margin: 40px;
    border: 1px solid #d8d8d8;
  }

  input {
    width: 100%;
    height: 25px;
    margin-bottom: 20px;
  }

  textarea {
    width: 100%;
    height: 60px;
  }

  .tab {
    margin-left: 20px;
    cursor: pointer;
  }

  .activeTab {
    color: #16C0B0;
    text-decoration: underline;
  }
</style>