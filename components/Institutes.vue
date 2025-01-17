<template>
    <div
      v-bind:class="{
        'bg-main': filled,
      }"
    >
      <hr v-if="separator" />
      <ul
        class="!list-none ns-c-tight"
        v-bind:class="{
          'justify-start': x === 'l',
          'justify-end': x === 'r',
        }"
      >
        <li v-for="(footnote, index) in footnotes" :key="index" class="whitespace-nowrap">
          <sup v-if="footnote.number && numbers">{{ footnote.number }}</sup>
          {{ footnote.content }}
        </li>
      </ul>
    </div>
  </template>
  
  <script setup lang="ts">
  import { PropType } from 'vue';
  
  interface Institute {
    number?: number;
    content: string;
  }
  
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
      default: 'r',
      type: String as PropType<'l' | 'r'>,
      validator: (value) => ['l', 'r'].includes(value),
    },
    footnotes: {
      type: Array as PropType<Institute[]>,
      default: () => [],
    },
    numbers: {
      default: true,
      type: Boolean,
    }
  });
  </script>

  <style scoped>
  li {
    margin-left: 0;
  }
  ul {
    font-size: 12pt;
  }
  </style>
