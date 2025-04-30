<script setup>
import { ref } from 'vue';

  const date = ref(new Date().toLocaleString())
</script>
<template>
  {{ date }}
</template>

<style scoped></style>
