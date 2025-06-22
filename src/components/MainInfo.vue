<script setup>
import Iconlocations from "../Icons/Iconlocations.vue";
import {ref, inject, watch, computed} from "vue";
import {activeDayProvide, locationNameProvide, nameOfMotht} from "../constans.js";

const city = ref(inject(locationNameProvide));
const dateData = inject(activeDayProvide);
const changedDay = ref();
const dayOfWeek = computed(() => {
  if (changedDay.value) {
    const thisDay = new Date(changedDay.value).toLocaleDateString('ru-RU', {weekday: 'long'});
    return thisDay.slice(0, 1).toUpperCase() + thisDay.slice(1);
  } else {
    return  '-'
  }

})

const activeDay = computed(() => {
  if (changedDay.value) {
    const day = new Date(changedDay.value).getDate();
    const month = nameOfMotht[new Date(changedDay.value).getMonth() + 1].slice(0, -1) + 'я';
    const year  = new Date(changedDay.value).getFullYear();
    return day + ' ' + month + ' ' + year
  } else {
    return  '-'
  }
})

watch([dateData,city], () => {
  changedDay.value = dateData.value?.date;
})

</script>

<template>
  <div class="main-info">
    <div class="main-info__day-week">{{ dayOfWeek }}</div>
    <div class="main-info__date">{{ activeDay !== 'NaN' ? activeDay : '-' }}</div>
    <div class="main-info__city">
      <div class="main-info__city-icon">
        <Iconlocations/>
      </div>
      {{ city ? city : '-' }}
    </div>
  </div>
</template>

<style scoped>
.main-info__day-week {
  font-size: 37px;
  font-weight: 700;
  margin-bottom: 16px;
}

.main-info__date {
  font-size: 22px;
  font-weight: 500;
  margin-bottom: 13px;
}

.main-info__city {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 20px;
  font-weight: 600;
}

.main-info__city-icon {
  display: flex;
}


</style>