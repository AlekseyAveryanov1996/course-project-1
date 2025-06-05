<script setup>
  const { label = "Не задано", stat="Нет информации" }  = defineProps({
    label: String,
    stat: String,
  })
</script>

<template>
  <div class="stat">
    <div class="stat__title">{{ label }}</div>
    <div class="stat__value">{{ stat }}</div>
  </div>
</template>

<style scoped>
  .stat {
    display: flex;
    align-items: center;
    gap: 20px;
    justify-content: space-between;
  }
  .stat__title {
    font-size: 28px;
    line-height: 100%;
    font-weight: 700;
    text-transform: uppercase;
  }
  .stat__value {
    font-size: 28px;
    line-height: 100%;
    font-weight: 500;
  }
</style>
