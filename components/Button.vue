<script setup lang="ts">
const emit = defineEmits<{
  (e: 'click', event: MouseEvent): void
}>();

const handleClick = (e: MouseEvent) => {
  emit('click', e);
};
</script>

<template>
  <button
      class="bg-azisaba-slate-tail cursor-pointer duration-150 flex gap-2 items-center px-4 py-2 text-sm text-white rounded-xl transition-colors
           hover:bg-azisaba-slate-tail/80 hover:outline-1 hover:outline-offset-1 hover:outline-azisaba-slate-tail"
      type="button"
      @click="handleClick"
  >
    <slot/>
  </button>
</template>

<style scoped>
</style>
