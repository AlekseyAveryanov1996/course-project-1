<script setup>
  import { useSlots } from 'vue';

  const slots = useSlots();
  const hasIconSlot = !!slots.icon;
</script>

<template>
  <button :class='hasIconSlot ? "button button_icon" : "button"'>
    <div>
      <slot name='icon' />
    </div>
    <slot />
  </button>
</template>

<style scoped>
  .button {
    padding: 14px;
    border-radius: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
    font-size: 20px;
    line-height: 100%;
    font-weight: 600;
    color: var(--colorWhite);
    background: var(--gradient1);
    outline: none;
    border: none;
    cursor: pointer;
    flex-grow: 1;
  }

  .button_icon {
    padding-top: 7px;
    padding-bottom: 8px;
  }

  .button:hover {
    animation: changeGradient 1s forwards;
  }

  @keyframes changeGradient {
      to {
          background: var(--gradient2);
      }
  }

</style>
