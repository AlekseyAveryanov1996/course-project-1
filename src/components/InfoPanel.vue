<script
    setup>
/*eslint no-undef: "error"*/

import Stat from './Stat.vue';
import CitySelect from './CitySelect.vue';
import NotFoundCity from './NotFoundCity.vue';
import {
  computed, ref
} from 'vue';
import CardStat from './CardStat.vue';


const API_ENDPOINT = "http://api.weatherapi.com/v1"
const errorMap = new Map([[1006, 'Указанный город не найден']])

const dataDefault = ref();
const isError = ref();
const activeIndex = ref(0);


const erorDisplay = computed(() => {
  return errorMap.get(isError.value?.error?.code)
})

async function getSity(city) {
  const params = new URLSearchParams({
    q: city, lang: "ru", key: '2987b812bbb8497fbd2131729251806', days: 4,
  })
  const res = await fetch(`${API_ENDPOINT}/forecast.json?${params.toString()}`)

  if (res.status !== 200) {
    isError.value = await res.json();
    dataDefault.value = null;
    return
  } else {
    isError.value = undefined;
  }

  dataDefault.value = await res.json();

}


const dataModified = computed(() => {
  if (!dataDefault.value) {
    return [];
  } else {
    return [{
      label: 'Влажность', stat: dataDefault.value.current.humidity + "%",
    }, {
      label: 'Облачность', stat: dataDefault.value.current.cloud + "%",
    }, {
      label: 'Ветер', stat: dataDefault.value.current.wind_kph + " км/ч",
    },]
  }
})

const dataWeather = computed(() => {
  if (!dataDefault.value) {
    return []
  } else {
    return dataDefault.value.forecast.forecastday
  }
})


</script>

<template>
  <div
      class="info-panel">

    <NotFoundCity
        v-if="isError"
        :label-error='erorDisplay'></NotFoundCity>

    <div
        v-else
        class="info-panel__main">
      <div
          class="stat-wrapper">
        <Stat
            v-for='(item, key) in dataModified'
            v-bind="item"
            :key='key'></Stat>
      </div>

      <div
          class="stat-weather">

        <CardStat
            v-for="(item, index) in dataWeather"
            :key='index'
            :day-of-week='new Date(item.date)'
            :temp='item.day.avgtemp_c'
            :number-code-weather='item.day.condition.code'
            :is-active='activeIndex === index'
            @click="() => activeIndex = index"/>
      </div>

    </div>

    <CitySelect
        @select-city='getSity'></CitySelect>
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

.stat-weather {
  display: flex;
  margin-top: 80px;
  gap: 1px;
}

</style>
