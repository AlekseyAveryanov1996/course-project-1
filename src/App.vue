<template>
  <div>
    {{ date }}
  </div>
</template>

<script setup>
  import { ref } from 'vue';
  const date = ref(new Date().toLocaleString());
</script>
