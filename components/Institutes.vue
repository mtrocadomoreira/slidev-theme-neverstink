<template>
    <div
      class="footnote-container left-0"
      v-bind:class="{
        'bg-main': filled,
      }"
    >
      <hr v-if="separator" />
      <ul
        class="!list-none p-2 ns-c-tight"
        v-bind:class="{
          'justify-start': x === 'l',
          'justify-end': x === 'r',
        }"
      >
        <li v-for="(footnote, index) in footnotes" :key="index" class="whitespace-nowrap pl-25">
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
.footnote-container .bg-main {
  background-color: #f0f0f0;
}

.footnote-container {
    margin-top: 1em;
    width: 60%;
    text-align: bottom;
}

.footnote-container hr {
  margin: 0.25rem 0;
  border-top: 1px solid #cccccccf;
}

.footnote-container ul {
  list-style-type: none;
  padding: 1px;
  margin: 0;
  
}

.footnote-container li {
  margin: 0.05rem 0rem;
  padding-bottom: 0.5rem;
  font-size: 1.25rem;
  font-size: 14pt;
  font-weight: light;
}

.footnote-container sup {
  font-weight: light;
  margin-right: 4px;

}
</style>