<script setup>
import { computed } from 'vue'
const props = defineProps({
  color: {
    default: 'light',
  },
  speed: {
    default: 0.5,
  },
  loop: {
    default: false,
  },
})

const colorscheme = computed(() => {
  return `neversink-${props.color}-scheme`
})
</script>
<template>
  <div class="slidecolor slidev-layout full flex flex-col" :class="colorscheme">
    <div class="w-full h-full">
      <CreditScroll :speed="props.speed" :loop="props.loop">
        <slot name="default"></slot>
      </CreditScroll>
    </div>
  </div>
</template>

<style scoped>
.quote {
  background-color: var(--neversink-bg-color);
  color: var(--neversink-text-color);
  border-color: var(--neversink-border-color);
}
</style>
