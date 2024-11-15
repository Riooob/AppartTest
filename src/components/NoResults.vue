<template>
    <div class="no-results">
      <h2>По вашему запросу ничего не найдено</h2>
      <p>Попробуйте изменить фильтры или поиск.</p>
    </div>
  </template>

<script>
export default {
  name: 'NoResults'
}
</script>

  <style scoped>
  .no-results {
    margin-top: 32px;
    text-align: center;
    color: #6c757d;
  }

  .no-results h2 {
    font-size: 1.5em;
    margin-bottom: 16px;
  }

  .no-results p {
    font-size: 1em;
  }
  </style>
