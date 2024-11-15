<template>
    <div>
      <div v-for="type in uniqueTypes" :key="type">
        <label>
          <input type="checkbox" :value="type" v-model="selectedTypes" />
          {{ type }}
        </label>
      </div>
    </div>
  </template>

<script>
import hotelsData from '@/hotels.json'

export default {
  name: 'HotelTypeFilter',
  data () {
    return {
      selectedTypes: []
    }
  },
  computed: {
    uniqueTypes () {
      const types = new Set(hotelsData.hotels.map(hotel => hotel.type))
      return Array.from(types)
    }
  },
  watch: {
    selectedTypes (newTypes) {
      this.$emit('update:types', newTypes)
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
