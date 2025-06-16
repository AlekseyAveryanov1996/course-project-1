<script setup>
  const { placeholder = 'Значение Поля' } = defineProps({
    placeholder: String,
  })
  const data = defineModel({
    type: String,
    required: true,
    default: 'Введите город',
  });

</script>

<template>
  <input v-model='data' type="text" class="Input" :placeholder='placeholder'>
</template>

<style scoped>
  input {
    padding: 15px 20px;
    border-radius: 10px;
    color: var(--colorWhite);
    font-size: 18px;
    font-weight: 400;
    background: var(--colorBlack2);
    border: none;
    outline: none;
  }
  input::placeholder {
    color: var(--colorTextInput);
  }
</style>
