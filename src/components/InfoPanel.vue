<script setup>
  import Stat from './Stat.vue';
  import CitySelect from './CitySelect.vue';
  import { computed, ref } from 'vue';

  const API_ENDPOINT = "http://api.weatherapi.com/v1"

  const dataDefault = ref()


  async function getSity(city) {
    const params = new URLSearchParams({
      q: city,
      lang: "ru",
      key: '2987b812bbb8497fbd2131729251806',
      days: 3,
    })
    const res = await fetch(`${API_ENDPOINT}/forecast.json?${params.toString()}`)
    dataDefault.value = await res.json();
    console.log(dataDefault.value)
  }

  const dataModified = computed(() => {
    if (!dataDefault.value) {
      return [];
    } else {
      return [{
        label: 'Влажность',
        stat: dataDefault.value.current.humidity + "%",
      },
      {
        label: 'Облачность',
        stat: dataDefault.value.current.cloud + "%",
      },
      {
        label: 'Ветер',
        stat: dataDefault.value.current.wind_kph + " км/ч",
      },
      ]
    }
  })

</script>

<template>
  <div class="info-panel">
    <div class="stat-wrapper">
      <Stat v-for='(item, key) in dataModified' v-bind="item" :key='key' ></Stat>
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
