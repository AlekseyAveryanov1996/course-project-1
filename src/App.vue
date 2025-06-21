<script setup>
  import LeftPanel from './components/LeftPanel.vue';
  import InfoPanel from './components/InfoPanel.vue';
  import Button from "./components/Button.vue";
</script>

<template>
  <div class="wrapper-pannel">
    <LeftPanel></LeftPanel>
    <InfoPanel></InfoPanel>
  </div>
</template>

<style scoped>
  .wrapper-pannel {
    display: flex;
    max-width: 944px;
    margin-left: auto;
    margin-right: auto;
    border-radius: 25px;
    background: var(--colorBlack);
    width: 100%;
    min-height: 623px;
    position: relative;
  }
</style>
