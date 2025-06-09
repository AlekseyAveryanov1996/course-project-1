<script setup>
  import Button from "./Button.vue";
  import Iconlocations from '../Icons/Iconlocations.vue';
  import Input from "./Input.vue";

  const emit = defineEmits({
    selectCity: function(payload) {
      return Boolean(payload);
    },
  })

  function select() {
    emit('selectCity', {
      city: 'London',
    });
  }
</script>

<template>
  <div class="citySelect">
    <Button @click="select()">
      <template #icon>
        <Iconlocations />
      </template>
      Изменить город
    </Button>
    <div class="citySelect__input-wrapper">
      <Input placeholder='Введите город'/>
      <Button>Сохранить</Button>
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
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    width: 100%;
    display: flex;
    gap: 12px;
  }
</style>
