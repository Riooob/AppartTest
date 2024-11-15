<template>
    <div>
      <input
        v-model.number="minReviews"
        type="number"
        placeholder="Например, от 10"
        class="reviews-input" />
    </div>
  </template>

<script>
export default {
  name: 'HotelReviewsFilter',
  data () {
    return {
      minReviews: null
    }
  },
  watch: {
    minReviews (newMinReviews) {
      this.$emit('update:reviews', newMinReviews)
    }
  }
}
</script>

  <style scoped>
  .reviews-input {
    margin-bottom: 16px;
    padding: 8px;
    width: 100%;
    box-sizing: border-box;
  }
  </style>
