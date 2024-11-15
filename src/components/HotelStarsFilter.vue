<template>
    <div>
      <div v-for="star in uniqueStars" :key="star">
        <label>
          <input type="checkbox" :value="star" v-model="selectedStars" />
          {{ star }} звезд
        </label>
      </div>
    </div>
  </template>

<script>
import hotelsData from '@/hotels.json'

export default {
  name: 'HotelStarsFilter',
  data () {
    return {
      selectedStars: []
    }
  },
  computed: {
    uniqueStars () {
      const stars = new Set(hotelsData.hotels.map(hotel => hotel.stars))
      return Array.from(stars).sort((a, b) => a - b)
    }
  },
  watch: {
    selectedStars (newStars) {
      this.$emit('update:stars', newStars)
    }
  }
}
</script>

  <style scoped>
  label {
    display: block;
    margin-bottom: 8px;
  }
  </style>
