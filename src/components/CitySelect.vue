<script setup>
import Button from "./Button.vue";
import Iconlocations from '../Icons/Iconlocations.vue';
import Input from "./Input.vue";
import {inject, ref} from "vue";
import {cityProvide} from "../constans.js";

const city = inject(cityProvide);
const inputCity = ref(city.value)
const isEdited = ref(false);


function changeCity() {
  isEdited.value = !isEdited.value
  city.value = inputCity.value;
}


</script>

<template>
  <div class="citySelect">
    <Button v-if="!isEdited" @click="changeCity()">
      <template #icon>
        <Iconlocations/>
      </template>
      Изменить город
    </Button>
    <div v-else class="citySelect__input-wrapper">
      <Input v-model='inputCity' placeholder='Введите город'
             @keyup.enter='() => { changeCity()}'
             v-focus/>
      <Button @click='() => {changeCity()}'>Сохранить</Button>
    </div>
  </div>
</template>

<style scoped>
.citySelect {
  position: relative;
  width: 100%;
  display: flex;
  margin-top: auto;
}

.citySelect__input-wrapper {
  width: 100%;
  display: flex;
  gap: 12px;
}
</style>
