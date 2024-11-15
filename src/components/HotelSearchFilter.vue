<template>
  <div>
    <input v-model="searchQuery" type="text" placeholder="Поиск по стране" class="search-input" />
  </div>
</template>

<script>
export default {
  name: 'HotelSearchFilter',
  data () {
    return {
      searchQuery: ''
    }
  },
  watch: {
    searchQuery (newQuery) {
      this.$emit('update:search-country', newQuery)
    }
  }
}
</script>

<style scoped>
.search-input {
  margin-bottom: 16px;
  padding: 8px;
  width: 100%;
  box-sizing: border-box;
}
</style>
