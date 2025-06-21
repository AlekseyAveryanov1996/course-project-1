<script setup>
import LeftPanel from './components/LeftPanel.vue';
import InfoPanel from './components/InfoPanel.vue';
import {provide, ref} from "vue";

const API_ENDPOINT = "http://api.weatherapi.com/v1"

const dataDefault = ref();
const isError = ref();
const activeIndex = ref(0);

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

provide('activeIndex', activeIndex);
provide('isError', isError);
provide('getCity', getSity)


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
