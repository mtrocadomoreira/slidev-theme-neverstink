<template>
  <div id="footnotes" class="content-container footnotes h-auto ns-c-tight">
    <hr v-if="separator"/>
    <ul
      class="auto flex-wrap !list-none pt-0 mt-0"
      v-bind:class="{
        'justify-start': x === 'l',
        'justify-end': x === 'r',
      }"
    >
      <slot />
    </ul>
  </div>
</template>

<script setup lang="ts">
import { PropType } from 'vue';

defineProps({
  filled: {
    default: false,
    type: Boolean,
  },
  separator: {
    default: false,
    type: Boolean,
  },
  x: {
    default: 'l',
    type: String as PropType<'l' | 'r'>,
    validator: (value) => value === 'l' || value === 'r',
  },
});
</script>
