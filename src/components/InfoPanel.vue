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

const {dataDefault} = defineProps({
  dataDefault: Object,
})

const activeIndexProvide = inject('activeIndex');
const isErrorProvide = inject('isError');
const errorMap = new Map([[1006, 'Указанный город не найден']])

const errorDisplay = computed(() => {
  return errorMap.get(isErrorProvide.value.error?.code)
})

const dataModified = computed(() => {
  if (!dataDefault) {
    return [];
  } else {
    return [{
      label: 'Влажность', stat: dataDefault.current.humidity + "%",
    }, {
      label: 'Облачность', stat: dataDefault.current.cloud + "%",
    }, {
      label: 'Ветер', stat: dataDefault.current.wind_kph + " км/ч",
    },]
  }
})

const dataWeather = computed(() => {
  if (!dataDefault) {
    return []
  } else {
    return dataDefault.forecast.forecastday
  }
})


</script>

<template>
  <div
      class="info-panel">

    <NotFoundCity
        v-if="isErrorProvide"
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
            :is-active='activeIndexProvide === index'
            @click="() => activeIndexProvide = index"/>
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
