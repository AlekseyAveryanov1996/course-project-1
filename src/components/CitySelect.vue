<script setup>
import Button from "./Button.vue";
import Iconlocations from '../Icons/Iconlocations.vue';
import Input from "./Input.vue";
import {inject, onMounted, ref} from "vue";


const getCityProvide = inject("getCity");
const isEdited = ref(false);
const city = ref('Тула')

function changeCity() {
  isEdited.value = !isEdited.value
}

onMounted(() => {
  getCityProvide(city.value);
})

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
      <Input v-model='city' placeholder='Введите город'
             @keyup.enter='() => {getCityProvide(city); changeCity()}'
             v-focus/>
      <Button @click='() => {getCityProvide(city); changeCity()}'>Сохранить</Button>
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
