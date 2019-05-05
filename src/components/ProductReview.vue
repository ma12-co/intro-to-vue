<template>
<form class="review-form">
    <p>
        <label for="name ">Name:</label>
        <input id="name" v-model="name">
    </p>
    <p>
        <label for="review">Review:</label>
        <textarea id="review" v-model="review"></textarea>
    </p>
    <p>
        <label for="rating">Rating:</label>
        <select id="rating" v-model.number="rating">
            <option>5</option>
            <option>4</option>
            <option>3</option>
            <option>2</option>
            <option>1</option>
        </select>
    </p>
</form>
</template>

<script>
export default {

    name: 'ProductReview',

    data() {
      return { 
          name: null,
          review: null,
          rating: null
    }
    }
}
</script>

<style scoped>

</style>
