<template>
  <div id="app">
    <HotelFilter
      @apply-filters="applyFilters"
      @clear-filters="clearFilters"
    />
    <HotelList
      :appliedFilters="appliedFilters"
    />
  </div>
</template>

<script>
import HotelFilter from '@/components/HotelFilter.vue'
import HotelList from '@/components/HotelList.vue'

export default {
  name: 'App',
  components: {
    HotelFilter,
    HotelList
  },
  data () {
    return {
      appliedFilters: {
        searchCountry: '',
        selectedCountries: [],
        selectedTypes: [],
        selectedStars: [],
        minReviews: null,
        minPrice: null,
        maxPrice: null
      }
    }
  },
  methods: {
    applyFilters (filters) {
      this.appliedFilters = { ...filters }
    },
    clearFilters () {
      this.appliedFilters = {
        searchCountry: '',
        selectedCountries: [],
        selectedTypes: [],
        selectedStars: [],
        minReviews: null,
        minPrice: null,
        maxPrice: null
      }
    }
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
