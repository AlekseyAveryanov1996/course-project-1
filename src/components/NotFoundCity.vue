<script setup>
  const props = defineProps({
    labelError: String,
  })
</script>
<template>
  <div class="not-city">
    {{ props.labelError }}
  </div>
</template>

<style>
  .not-city {
    padding: 15px 52px;
    text-align: center;
    font-size: 18px;
    color: var(--colorWhite);
    background: var(--colorBlack2);
    border-radius: 0 0 12px 12px;
    position: absolute;
    top: 0;
    right: 60px;
  }
</style>
