<template>
  <li class="text-10pt whitespace-nowrap">
    <sup v-if="number">{{ number }}&nbsp;</sup> 
    <slot />
  </li>
</template>

<script setup lang="ts">
defineProps<{
  number?: number;
}>();
</script>
