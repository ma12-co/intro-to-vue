<template>
  <div class="product">
      <div class="product-image">
        <img :src="image">
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inventory > 10">In stock</p>
        <p v-else-if="inventory <= 10 && inventory >0">Almost sold out!</p>
        <p 
        v-if="inventory === 0"
        >Out of stock</p>
        <p>User is premium: {{isPremium.required}}</p>
        <ul>
          <li :key="detail" v-for="detail in details">{{detail}}</li>
        </ul>

        <div 
          :key='variant' 
          v-for="(variant, index) in variants"
          class="color-box"
          :style="{ backgroundColor: variant.variantColor }"
          @mouseover="updateProduct(index)">
        </div>

        <button 
        v-on:click="addToCart" 
        :disabled="!inStock"
        :class="{ disabledButton : !inStock}">
        Add to cart</button>
        <div class="cart">
          <p>Cart({{cart}})</p>
        </div>
      </div>
    </div>
</template>

<script>

export default {
  name: 'Product',
  data() {
      return {
        brand: "Vue Mastery",
        product: "socks",
        selectedVariant: 0,
        
        variants: [
          {
            variantId: 2234,
            variantColor: 'green',
            variantImage: require('../assets/vmSocks-green.jpg'),
            variantQuantity: 5

          },
          {
            variantId: 2235,
            variantColor: 'blue',
            variantImage: require('../assets/vmSocks-blue.jpg'),
            variantQuantity: 10

          }
        ],
        cart: 0
      }
    },
    methods: {
      addToCart: function() {
        this.cart++
      },
      updateProduct: function(index)  {this.selectedVariant = index
      }
    },
    computed: {
      title() {
        return `${this.brand} ${this.product}`
      },
      image() {
        return this.variants[this.selectedVariant].variantImage
      },
      inStock() {
        return this.variants[this.selectedVariant].variantQuantity>0
      }
    },
  props: [
    'isPremium',
    'details'
  ]
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
