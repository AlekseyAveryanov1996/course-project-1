<script setup>
  import Button from "./Button.vue";
  import Iconlocations from '../Icons/Iconlocations.vue';
  import Input from "./Input.vue";
  import { ref } from "vue";

  const emit = defineEmits({
    selectCity: function(payload) {
      return Boolean(payload);
    },
  })

  const isEdited = ref(false);

  function select() {
    emit('selectCity', 'London');
  }

  function changeCity() {
    isEdited.value = !isEdited.value
  }

</script>

<template>
  <div class="citySelect">
    <Button @click="changeCity()" v-if="!isEdited">
      <template #icon>
        <Iconlocations />
      </template>
      Изменить город
    </Button>
    <div class="citySelect__input-wrapper" v-else>
      <Input placeholder='Введите город'/>
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
