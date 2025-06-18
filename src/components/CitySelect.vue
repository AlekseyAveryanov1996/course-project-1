<script setup>
  import Button from "./Button.vue";
  import Iconlocations from '../Icons/Iconlocations.vue';
  import Input from "./Input.vue";
  import { onMounted, ref } from "vue";



  const emit = defineEmits({
    selectCity: function(payload) {
      return Boolean(payload);
    },
  })

  const isEdited = ref(false);
  const city = ref('Moscow')

  function select() {
    emit('selectCity', city.value);
  }

  function changeCity() {
    isEdited.value = !isEdited.value
  }

  onMounted(() => {
    select();
  })



</script>

<template>
  <div class="citySelect">
    <Button v-if="!isEdited" @click="changeCity()" >
      <template #icon>
        <Iconlocations />
      </template>
      Изменить город
    </Button>
    <div v-else class="citySelect__input-wrapper">
      <Input v-model='city' placeholder='Введите город' @keyup.enter='() => {select(); changeCity()}'/>
      <Button @click='() => {select(); changeCity()}'>Сохранить</Button>
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
