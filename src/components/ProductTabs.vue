<template>
  <div>
    <span 
      class="tabs"
      :class="{activeTab: selectedTab === tab}" 
      v-for="(tab,index) in tabs" 
      :key="index"
      @click="selectedTab = tab"
      >
      {{tab}}
      </span>

      <div v-show="selectedTab ==='Reviews'">
        <h2>Reviews</h2>
        <p v-if="!reviews.length">There are no reviews yet.</p>
        <ul>
          <li :key="review.review" v-for="review in reviews">
          <p>{{review.name}}</p> 
          <p>Rating: {{review.rating}}</p>  
          <p>{{review.review}}</p>  
            
          </li>
        </ul>
      </div>

      <ProductReview v-show="selectedTab ==='Make a Review'"/>
  </div>
</template>


<script>
import ProductReview from "./ProductReview.vue"


export default {
  name: "ProductTabs",
  data() {
    return {
      tabs: ["Reviews", "Make a Review"],
      selectedTab: 'Reviews'
    };
  },
  props: {
    reviews: {
      type: Array,
      required: true
    }
  },
  components: {
    ProductReview,
  }
  
};
</script>


<style scoped>
</style>

