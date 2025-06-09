<script setup>
  import Stat from './Stat.vue';
  import CitySelect from './CitySelect.vue';
  import { computed, ref } from 'vue';

  let savedCity = ref('Москва');

  const dataDefault = ref({
    humidity: 90,
  })


  function getSity(data) {
    savedCity.value = data;
    dataDefault.value.humidity = 20;
  }

  const dataModified = computed((prev) => {
    console.log(prev);
    return {
      label: 'Влажность',
      stat: dataDefault.value.humidity + "%",
    }
  })

</script>

<template>
  <div class="info-panel">
    <div id="city">{{ savedCity }}</div>
    <div class="stat-wrapper">
      <Stat v-bind='dataModified'></Stat>
      <Stat label='Осадки' stat='0%'></Stat>
      <Stat label='Ветер' stat='3 м/ч'></Stat>
    </div>
    <CitySelect @select-City='getSity'></CitySelect>
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
