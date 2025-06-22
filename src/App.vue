<script setup>
import LeftPanel from './components/LeftPanel.vue';
import InfoPanel from './components/InfoPanel.vue';
import {computed, onMounted, provide, ref, watch} from "vue";
import {
  activeDayProvide, activeIndexProvide, cityProvide, isErrorProvide, locationNameProvide
} from "./constans.js";

const API_ENDPOINT = "http://api.weatherapi.com/v1"

const dataDefault = ref();
const isError = ref();
const activeIndex = ref(0);
const city = ref('Тула')

const locationName = computed(() => {
  return dataDefault.value?.location?.name
})

const activeDayData = computed(() => {
  return dataDefault.value?.forecast?.forecastday[activeIndex.value]
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

onMounted( () => {
  getSity(city.value);
})

watch(city, () => {
  getSity(city.value);
})

provide(activeIndexProvide, activeIndex);
provide(isErrorProvide, isError);
provide(cityProvide, city)
provide(locationNameProvide, locationName)
provide(activeDayProvide, activeDayData)





</script>

<template>
  <div class="wrapper-pannel">
    <LeftPanel></LeftPanel>
    <InfoPanel
        :active-index="activeIndex"
        :data-default="dataDefault"
        :is-error="isError"
        @get-city="getSity">
    </InfoPanel>
  </div>
</template>


<style scoped>
.wrapper-pannel {
  display: flex;
  max-width: 944px;
  margin-left: auto;
  margin-right: auto;
  border-radius: 25px;
  background: var(--colorBlack);
  width: 100%;
  min-height: 623px;
  position: relative;
}
</style>
