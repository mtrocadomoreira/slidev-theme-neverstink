<script setup>
import { computed } from 'vue'
import { Icon } from '@iconify/vue'
const props = defineProps({
  color: {
    type: String,
    default: 'amber-light',
  },
  title: {
    type: String,
    default: 'Note',
  },
  icon: {
    type: String,
    default: 'mdi-information-variant-circle-outline',
  },
  width: {
    type: String,
    default: '100%',
  },
})

const colorscheme = computed(() => {
  return `neversink-${props.color}-scheme`
})
</script>

<template>
  <div class="markdown-alert markdown-alert-custom" :class="colorscheme">
    <p class="markdown-alert-title-custom">
      <span class="font-size-1.3rem"><Icon :icon="props.icon" /></span>&nbsp;&nbsp;{{ props.title }}
    </p>
    <p><slot></slot></p>
  </div>
</template>

<style scoped>
.markdown-alert {
  padding: 8px 16px;
  margin: 10px;
  margin-left: 0;
  margin-top: 2px;
  margin-bottom: 16px;
  color: inherit;
  border-radius: 6px;
  width: v-bind(props.width);
  font-family: var(--neversink-main-font);
}

.markdown-alert p:not(first-child) {
  margin: 0;
  margin-bottom: 2px;
  font-size: 0.85rem;
}
.markdown-alert > :first-child {
  margin-top: 0;
}
.markdown-alert > :last-child {
  margin-bottom: 2px;
}
.markdown-alert.markdown-alert-custom {
  background-color: var(--neversink-admon-bg-color);
  color: var(--neversink-admon-text-color);
  border: 2px solid var(--neversink-admon-border-color);
  border-left: 7px solid var(--neversink-admon-border-color);
}
.markdown-alert .markdown-alert-title-custom {
  display: flex;
  align-items: center;
  position: relative;
  font-weight: 700;
  color: var(--neversink-admon-text-color);
  font-size: 1rem;
  margin-bottom: 8px;
}
@media print {
  .markdown-alert .markdown-alert-title:before {
    display: none;
  }
}
</style>
