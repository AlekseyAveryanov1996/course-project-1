<script
    setup>
/*eslint no-undef: "error"*/

import Stat from './Stat.vue';
import CitySelect from './CitySelect.vue';
import NotFoundCity from './NotFoundCity.vue';
import {
  computed, inject,
} from 'vue';
import CardStat from './CardStat.vue';
import {activeIndexProvide, isErrorProvide} from "../constans.js";

const {dataDefault} = defineProps({
  dataDefault: Object,
})

const activeIndex = inject(activeIndexProvide);
const isError = inject(isErrorProvide);
const errorMap = new Map([[1006, 'Указанный город не найден']])

const errorDisplay = computed(() => {
  return errorMap.get(isError.value.error?.code)
})


const dataModified = computed(() => {
  if (!dataDefault) {
    return [];
  } else {
    return [{
      label: 'Влажность', stat: dataDefault.forecast.forecastday[activeIndex.value].day.avghumidity + "%",
    }, {
      label: 'Облачность', stat: dataDefault.forecast.forecastday[activeIndex.value].day.daily_chance_of_rain + "%",
    }, {
      label: 'Ветер', stat: dataDefault.forecast.forecastday[activeIndex.value].day.maxwind_kph + " км/ч",
    },]
  }
})

const dataWeather = computed(() => {
  if (!dataDefault) {
    return []
  } else {
    return dataDefault?.forecast?.forecastday
  }
})


</script>

<template>
  <div
      class="info-panel">

    <NotFoundCity
        v-if="isError"
        :label-error='errorDisplay'></NotFoundCity>

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
            :temp='item.day.maxtemp_c'
            :number-code-weather='item.day.condition.code'
            :is-active='activeIndex === index'
            @click="() => activeIndex = index"/>
      </div>

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

.stat-weather {
  display: flex;
  margin-top: 80px;
  gap: 1px;
}

</style>
