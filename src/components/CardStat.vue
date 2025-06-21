<script setup>
import { computed } from 'vue';
import SunIcon from '../Icons/weather/SunIcon.vue';
import CloudSunIcon from '../Icons/weather/CloudSunIcon.vue';
import RainIcon from '../Icons/weather/RainIcon.vue';

  const {numberCodeWeather, dayOfWeek, temp, isActive = false} = defineProps({
    numberCodeWeather: Number,
    dayOfWeek: Date,
    temp: Number,
    isActive: Boolean,
  })

  const activeIconProps = computed(() => {
    return isActive ? { color: '#000000', } : {color: 'white'};
  })

</script>

<template>
  <div :class='isActive ? "card-stat --active" : "card-stat"'>
    <div class="card-stat__icon">
      <SunIcon v-if='numberCodeWeather <=  1003' v-bind="activeIconProps" />
      <CloudSunIcon v-if='numberCodeWeather >= 1006 && numberCodeWeather < 1063' v-bind="activeIconProps" />
      <RainIcon v-if='numberCodeWeather >= 1063' v-bind="activeIconProps" />

    </div>
    <div class="card-stat__day">
      {{ dayOfWeek.toLocaleDateString('ru-RU', {weekday: 'short'}) }}
    </div>
    <div class="card-stat__temp">
      {{ temp + ' °C' }}
    </div>
  </div>
</template>

<style scoped>
  .card-stat {
    padding: 14px 21px 20px 21px;
    background: var(--colorBlack2);
    color: var(--colorWhite);
    display: flex;
    flex-direction: column;
    align-items: center;
    border-radius: 6px;
    cursor: pointer;
  }
  .card-stat__icon {
    width: 54px;
    height: 54px;
    display: flex;
  }
  .card-stat__day {
    font-size: 20px;
    text-align: center;
    margin-top: 16px;
  }
  .card-stat__temp {
    font-weight: 700;
    font-size: 18px;
    margin-top: 14px;
  }

  .card-stat:hover {
    background: var(--colorHover1);
  }

  .card-stat.--active {
    background: var(--colorWhite);
    color: var(--colorBlack)
  }

</style>
