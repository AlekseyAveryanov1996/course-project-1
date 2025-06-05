<script setup>
  import Stat from './Stat.vue';
  import CitySelect from './CitySelect.vue';


  const data = {
    label: 'Влажность',
    stat: '90%',
  }

</script>

<template>
  <div class="info-panel">
    <div class="stat-wrapper">
      <Stat v-bind='data'></Stat>
      <Stat label='Осадки' stat='0%'></Stat>
      <Stat label='Ветер' stat='3 м/ч'></Stat>
    </div>
    <CitySelect></CitySelect>
  </div>
</template>

<style scoped>
  .info-panel {
    padding: 55px 50px 62px 479px;
    width: 100%;
    display: flex;
    flex-direction: column;
  }
  .stat-wrapper {
    display: flex;
    flex-direction: column;
    gap: 16px;
  }
</style>
