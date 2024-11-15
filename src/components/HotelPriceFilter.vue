<template>
    <div>
      <div>
        <label>
          <span>От:</span>
          <input v-model.number="minPrice" type="number" placeholder="Минимальная цена" class="price-input" />
        </label>
        <label>
          <span>До:</span>
          <input v-model.number="maxPrice" type="number" placeholder="Максимальная цена" class="price-input" />
        </label>
      </div>
      <div class="range-container">
        <input
          type="range"
          :min="minPriceRange"
          :max="maxPriceRange"
          v-model.number="minPrice"
          class="price-range"
          @input="updateMinPrice"
        />
        <input
          type="range"
          :min="minPriceRange"
          :max="maxPriceRange"
          v-model.number="maxPrice"
          class="price-range"
          @input="updateMaxPrice"
        />
      </div>
    </div>
  </template>

<script>
import hotelsData from '@/hotels.json'

export default {
  name: 'HotelPriceFilter',
  data () {
    return {
      minPrice: null,
      maxPrice: null,
      minPriceRange: 0,
      maxPriceRange: 10000 // Установите максимальное значение в зависимости от ваших данных
    }
  },
  created () {
    this.minPriceRange = Math.min(...hotelsData.hotels.map(hotel => hotel.min_price))
    this.maxPriceRange = Math.max(...hotelsData.hotels.map(hotel => hotel.min_price))
    this.minPrice = this.minPriceRange
    this.maxPrice = this.maxPriceRange
  },
  methods: {
    updateMinPrice (event) {
      let newMinPrice = parseInt(event.target.value, 10)
      if (newMinPrice > this.maxPrice) {
        newMinPrice = this.maxPrice
      }
      this.minPrice = newMinPrice
      this.$emit('update:min-price', newMinPrice)
    },
    updateMaxPrice (event) {
      let newMaxPrice = parseInt(event.target.value, 10)
      if (newMaxPrice < this.minPrice) {
        newMaxPrice = this.minPrice
      }
      this.maxPrice = newMaxPrice
      this.$emit('update:max-price', newMaxPrice)
    }
  }
}
</script>

  <style scoped lang="scss">
  .price-input {
    margin-bottom: 8px;
    padding: 8px;
    width: 48%;
    box-sizing: border-box;
    display: inline-block;
  }

  .range-container {
    position: relative;
    width: 100%;
    margin-bottom: 16px;
  }

  .price-range {
    position: absolute;
    width: 100%;
    margin: 0;
    -webkit-appearance: none;
    appearance: none;
    background: transparent;
    pointer-events: none;
  }

  .price-range::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 16px;
    height: 16px;
    background: #007bff;
    border-radius: 50%;
    cursor: pointer;
    pointer-events: auto;
  }

  .price-range::-moz-range-thumb {
    width: 16px;
    height: 16px;
    background: #007bff;
    border-radius: 50%;
    cursor: pointer;
    pointer-events: auto;
  }

  .price-range::-webkit-slider-runnable-track {
    width: 100%;
    height: 4px;
    background: #ccc;
    border-radius: 2px;
  }

  .price-range::-moz-range-track {
    width: 100%;
    height: 4px;
    background: #ccc;
    border-radius: 2px;
  }

  span {
    margin-right: 8px;
  }
  .range-container {
  width: 200px;
  margin: auto 16px;
  text-align: center;
  position: relative;
  margin-bottom: 16px;
      svg, input[type=range] {
          position: absolute;
          left: 0;
          bottom: 0;
  }
}
input[type=range]::-webkit-slider-thumb {
  z-index: 2;
  position: relative;
  top: 2px;
  margin-top: -7px;
}
  </style>
