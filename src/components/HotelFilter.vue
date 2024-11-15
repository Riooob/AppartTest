<template>
  <div>
    <h2 @click="toggleSection('country')">Страна</h2>
    <div v-if="sectionsVisible.country">
      <HotelSearchFilter @update:search-country="updateSearchCountry" />
      <HotelCountryFilter
        :searchCountry="searchCountry"
        @update:countries="updateSelectedCountries"
      />
    </div>

    <h2 @click="toggleSection('type')">Тип</h2>
    <div v-if="sectionsVisible.type">
      <HotelTypeFilter @update:types="updateSelectedTypes" />
    </div>
    <h2 @click="toggleSection('stars')">Количество звезд</h2>
    <div v-if="sectionsVisible.stars">
      <HotelStarsFilter @update:stars="updateSelectedStars" />
    </div>
    <h2 @click="toggleSection('reviews')">Количество отзывов (от)</h2>
    <div v-if="sectionsVisible.reviews">
    <HotelReviewsFilter @update:reviews="updateMinReviews" />
    </div>
    <h2 @click="toggleSection('price')">Цена</h2>
    <div v-if="sectionsVisible.price">
    <HotelPriceFilter
      @update:min-price="updateMinPrice"
      @update:max-price="updateMaxPrice"
    />
    </div>

    <div class="button-container" v-if="isAnySectionVisible">
      <button @click="applyFilters" class="apply-button">Применить фильтр</button>
      <button @click="clearFilters" class="clear-button">Очистить фильтр</button>
    </div>
  </div>
</template>

<script>
import HotelSearchFilter from '@/components/HotelSearchFilter.vue'
import HotelCountryFilter from '@/components/HotelCountryFilter.vue'
import HotelTypeFilter from '@/components/HotelTypeFilter.vue'
import HotelStarsFilter from '@/components/HotelStarsFilter.vue'
import HotelReviewsFilter from '@/components/HotelReviewsFilter.vue'
import HotelPriceFilter from '@/components/HotelPriceFilter.vue'

export default {
  name: 'HotelFilters',
  components: {
    HotelSearchFilter,
    HotelCountryFilter,
    HotelTypeFilter,
    HotelStarsFilter,
    HotelReviewsFilter,
    HotelPriceFilter
  },
  data () {
    return {
      searchCountry: '',
      selectedCountries: [],
      selectedTypes: [],
      selectedStars: [],
      minReviews: null,
      minPrice: null,
      maxPrice: null,
      sectionsVisible: {
        country: false,
        type: false,
        stars: false,
        reviews: false,
        price: false
      }
    }
  },
  computed: {
    isAnySectionVisible () {
      return Object.values(this.sectionsVisible).some(visible => visible)
    }
  },
  methods: {
    updateSearchCountry (newQuery) {
      this.searchCountry = newQuery
    },
    updateSelectedCountries (newCountries) {
      this.selectedCountries = newCountries
    },
    updateSelectedTypes (newTypes) {
      this.selectedTypes = newTypes
    },
    updateSelectedStars (newStars) {
      this.selectedStars = newStars
    },
    updateMinReviews (newReviews) {
      this.minReviews = newReviews
    },
    updateMinPrice (newMinPrice) {
      this.minPrice = newMinPrice
    },
    updateMaxPrice (newMaxPrice) {
      this.maxPrice = newMaxPrice
    },
    applyFilters () {
      this.$emit('apply-filters', {
        searchCountry: this.searchCountry,
        selectedCountries: this.selectedCountries,
        selectedTypes: this.selectedTypes,
        selectedStars: this.selectedStars,
        minReviews: this.minReviews,
        minPrice: this.minPrice,
        maxPrice: this.maxPrice
      })
    },
    clearFilters () {
      this.searchCountry = ''
      this.selectedCountries = []
      this.selectedTypes = []
      this.selectedStars = []
      this.minReviews = null
      this.minPrice = null
      this.maxPrice = null
    },
    toggleSection (section) {
      this.sectionsVisible[section] = !this.sectionsVisible[section]
    }
  }
}
</script>

<style scoped>
h2 {
  cursor: pointer;
  margin-bottom: 8px;
}

.button-container {
  margin-top: 16px;
  display: flex;
  justify-content: space-between;
}

.apply-button, .clear-button {
  padding: 8px 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  cursor: pointer;
  background-color: #007bff;
  color: white;
  margin-right: 8px;
}

.clear-button {
  background-color: #6c757d;
}

.apply-button:hover, .clear-button:hover {
  opacity: 0.9;
}
</style>
