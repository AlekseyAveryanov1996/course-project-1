<script setup>
  import { ref } from 'vue';
  const date = ref(new Date().toLocaleString())
</script>

<template>
  <div>
    {{ date }}
  </div>
</template>

<style scoped></style>
