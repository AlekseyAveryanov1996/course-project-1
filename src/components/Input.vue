<script setup>
  const { placeholder = 'Значение Поля' } = defineProps({
    placeholder: String,
  })
</script>

<template>
  <input type="text" class="Input" :placeholder='placeholder'>
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
