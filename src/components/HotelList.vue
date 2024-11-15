<template>
  <div>
    <h1>Список отелей</h1>
    <div v-for="hotel in filteredHotels" :key="hotel.name" class="hotel-card">
      <h2>{{ hotel.name }}</h2>
      <p><strong>Страна:</strong> {{ hotel.country }}</p>
      <p><strong>Адрес:</strong> {{ hotel.address }}</p>
      <p><strong>Звезды:</strong> {{ hotel.stars }}</p>
      <p><strong>Тип:</strong> {{ hotel.type }}</p>
      <p><strong>Описание:</strong> {{ hotel.description }}</p>
      <p><strong>Услуги:</strong> {{ hotel.services.join(', ') }}</p>
      <p><strong>Минимальная цена:</strong> {{ hotel.min_price }} {{ hotel.currency }}</p>
      <p><strong>Рейтинг:</strong> {{ hotel.rating }}</p>
      <p><strong>Количество отзывов:</strong> {{ hotel.reviews_amount }}</p>
      <p><strong>Последний отзыв:</strong> {{ hotel.last_review }}</p>
      <button :class="buttonClass" @click="toggleColor">
        <p>{{ buttonText }}</p>
      </button>
    </div>
  </div>
</template>

<script>
import hotelsData from '@/hotels.json'

export default {
  name: 'HotelList',
  props: {
    appliedFilters: {
      type: Object,
      default: () => ({
        searchCountry: '',
        selectedCountries: [],
        selectedTypes: [],
        selectedStars: [],
        minReviews: null,
        minPrice: null,
        maxPrice: null
      })
    }
  },
  data () {
    return {
      hotels: hotelsData.hotels,
      isActive: false
    }
  },
  computed: {
    filteredHotels () {
      return this.hotels
        .filter(hotel =>
          hotel.country.toLowerCase().includes(this.appliedFilters.searchCountry.toLowerCase()) &&
          (this.appliedFilters.selectedCountries.length === 0 || this.appliedFilters.selectedCountries.includes(hotel.country)) &&
          (this.appliedFilters.selectedTypes.length === 0 || this.appliedFilters.selectedTypes.includes(hotel.type)) &&
          (this.appliedFilters.selectedStars.length === 0 || this.appliedFilters.selectedStars.includes(hotel.stars)) &&
          (this.appliedFilters.minReviews === null || hotel.reviews_amount >= this.appliedFilters.minReviews) &&
          (this.appliedFilters.minPrice === null || hotel.min_price >= this.appliedFilters.minPrice) &&
          (this.appliedFilters.maxPrice === null || hotel.min_price <= this.appliedFilters.maxPrice)
        )
        .slice(0, 3)
    },
    buttonClass () {
      return {
        'active-button': this.isActive,
        'default-button': !this.isActive
      }
    },
    buttonText () {
      return this.isActive ? 'Забронировано' : 'Забронировать'
    }
  },
  methods: {
    toggleColor () {
      this.isActive = !this.isActive
    }
  }
}
</script>

<style scoped lang="scss">
.hotel-card {
  border: 1px solid #ccc;
  padding: 16px;
  margin-bottom: 16px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
.active-button {
  border: none;
  background-color: rgba(74, 250, 124, 0.77);
  color: #00BB6D;
  border-radius: 12px;
}
.default-button {
  border: none;
  background-color: rgba(141, 74, 250, 0.37);
  color: #6A53F5;
  border-radius: 12px;
}

</style>
