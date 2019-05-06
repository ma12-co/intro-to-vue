<template>
  <div class="product">
      <div class="product-image">
        <img :src="image">
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock">In stock</p>
        <p v-if="!inStock">Out of stock</p>
        <p>User is premium: {{isPremium}}</p>
        <ul>
          <li :key="`${detail}-${index}`" v-for="(detail, index) in details">{{detail}}</li>
        </ul>

        <div 
          :key='`${variant}-${index}`' 
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
        
      </div>

      <ProductTabs :reviews="reviews"/>

      

    </div>
</template>

<script>
import ProductTabs from "./ProductTabs.vue"
import {EventBus} from "./EventBus.js"

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
        reviews:[]
        
      }
    },
    methods: {
      addToCart() {
        this.$emit('add-to-cart', this.variants[this.selectedVariant].variantId)
      },
      updateProduct: function(index)  {this.selectedVariant = index
      },
      
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
  ],
  components: {
    EventBus,
    ProductTabs
  },
  mounted() {
    EventBus.$on('revew-submitted', ProductReview => {
      this.reviews.push(ProductReview)
    })
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
