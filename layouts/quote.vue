<script setup>
import { computed } from 'vue'
const props = defineProps({
  color: {
    default: 'light',
  },
  author: {
    default: null,
  },
  quotesize: {
    default: 'text-2xl',
  },
  authorsize: {
    default: 'text-l',
  },
})

const colorscheme = computed(() => {
  return `neversink-${props.color}-scheme`
})
</script>
<template>
  <div class="slidev-layout slidev-layout--vertlines">
    <div class="slidev-layout section">
      <div class="slidev-layout section section-container quote">
        <div class="leading-normal pl-3.5em pr-3.5em">
          <div class="quote_text" :class="quotesize">
            <slot name="default" /><br />
          </div>
          <div v-if="author !== null" class="quote_author" :class="authorsize">&mdash; {{ author }}</div>
        </div>
      </div>
    </div>
    <Footer 
        :author="Object.keys($slidev.configs.authors[Object.keys($slidev.configs.authors)[0]])[0]" 
        :meeting="$slidev.configs.meeting"
        :date="$slidev.configs.date">
    </Footer>
  </div>
</template>

<style>
.quotecolor {
  background-color: var(--neversink-bg-color);
  color: var(--neversink-text-color);
  border-color: var(--neversink-border-color);
  /* add a drop shadow */
  box-shadow: 5px 4px 6px rgba(0, 0, 0, 0.1);
}

.quote_author {
  font-family: var(--neversink-title-font);
  font-weight: 400;
  text-align: right;
}

.quote_text {
  font-family: var(--neversink-quote-font);
}

</style>
