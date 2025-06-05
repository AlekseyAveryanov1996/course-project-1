<script setup>
  import Iconlocations from '../Icons/Iconlocations.vue';
  import Button from './Button.vue';
  import Stat from './Stat.vue';


  const data = {
    label: 'Влажность',
    stat: '90%',
  }

</script>

<template>
  <div class="info-panel">
    <div class="stat-wrapper">
      <Stat :='data'></Stat>
      <Stat label='Осадки' stat='0%'></Stat>
      <Stat label='Ветер' stat='3 м/ч'></Stat>
    </div>
    <Button>
      <template #icon>
        <Iconlocations />
      </template>

      Изменить город
    </Button>
  </div>
</template>

<style scoped>
  .info-panel {
    padding: 55px 50px 62px 479px;
    width: 100%;
  }
  .stat-wrapper {
    display: flex;
    flex-direction: column;
    gap: 16px;
  }
</style>
