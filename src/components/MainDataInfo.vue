<script setup>
import SunIcon from "../Icons/weather/SunIcon.vue";
import CloudSunIcon from "../Icons/weather/CloudSunIcon.vue";
import RainIcon from "../Icons/weather/RainIcon.vue";
import {computed, inject} from "vue";
import {activeDayProvide} from "../constans.js";

const dateData = inject(activeDayProvide);
const statusWeatherCode = computed(() => {
  return dateData.value?.day?.condition?.code;
})
const temp = computed(() => {
  return dateData.value?.day?.maxtemp_c;
})
const weatherText = computed(() => {
  return dateData.value?.day?.condition?.text;
})

</script>


<template>
  <div class="main-data">
    <div class="main-data__icon">
      <SunIcon v-if='statusWeatherCode <=  1003' v-bind="activeIconProps"/>
      <CloudSunIcon v-if='statusWeatherCode >= 1006 && statusWeatherCode < 1063'/>
      <RainIcon v-if='statusWeatherCode >= 1063' v-bind="statusWeatherCode"/>
    </div>
    <div class="main-data__temp">{{ temp ? temp + ' °C' : '-' }}</div>
    <div class="main-data__status">{{ weatherText }}</div>
  </div>
</template>

<style scoped>
.main-data {
  margin-top: auto;
}

.main-data__icon {
  display: flex;
  width: 95px;
  height: 95px;
  margin-bottom: 10px;
}

.main-data__icon svg {
  width: 100%;
  height: 100%;
}

.main-data__temp {
  font-size: 50px;
  font-weight: 700;
  margin-bottom: 13px;
}

.main-data__status {
  font-size: 30px;
  font-width: 700;
}


</style>