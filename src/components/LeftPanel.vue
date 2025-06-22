<script setup lang="ts">
import MainInfo from "./MainInfo.vue";
import MainDataInfo from "./MainDataInfo.vue";
</script>

<template>
  <div class="left-panel">
    <MainInfo/>
    <MainDataInfo />
  </div>
</template>

<style scoped>

.left-panel {
  min-height: 666px;
  border-radius: 30px;
  background-color: var(--gradient1);
  width: 493px;
  flex-shrink: 0;
  top: -21px;
  left: -69px;
  position: absolute;
  padding: 48px 48px 84px 32px;
  background-image: url('/src/assets/img.jpg');
  background-repeat: no-repeat;
  display: flex;
  flex-direction: column;
}
</style>
