<template>
  <div>
    <div v-if="filteredCountries.length > 0">
      <div v-for="country in filteredCountries" :key="country">
        <label>
          <input type="checkbox" :value="country" v-model="selectedCountries" />
          {{ country }}
        </label>
      </div>
    </div>
    <div v-else>
      <p>К сожалению, по вашему запросу ничего не найдено</p>
    </div>
  </div>
</template>

<script>
import hotelsData from '@/hotels.json'

export default {
  name: 'HotelCountryFilter',
  props: {
    searchCountry: {
      type: String,
      default: ''
    }
  },
  data () {
    return {
      selectedCountries: []
    }
  },
  computed: {
    uniqueCountries () {
      const countries = new Set(hotelsData.hotels.map(hotel => hotel.country))
      return Array.from(countries)
    },
    filteredCountries () {
      return this.uniqueCountries.filter(country =>
        country.toLowerCase().includes(this.searchCountry.toLowerCase())
      )
    }
  },
  watch: {
    selectedCountries (newCountries) {
      this.$emit('update:countries', newCountries)
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
