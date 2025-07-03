<script setup lang="ts">
import { computed } from 'vue'
import TitleRenderer from '#slidev/title-renderer'
import { compute_alignment, compute_column_size } from '../layoutHelper'

const props = defineProps({
  columns: {
    default: 'is-one-half',
  },
  align: {
    default: 'l-lt-lt',
  },
})

const colwidth = computed(() => compute_column_size(props.columns))

const alignment = computed(() => {
  const parts = props.align.split('-')
  return { t: compute_alignment(parts[0]), l: compute_alignment(parts[1]), r: compute_alignment(parts[2]) }
})
</script>

<template>
  <div class="slidev-layout slidev-layout--horlines">
    <div class="slidev-layout default col-start-2 col-span-3 row-start-2 row-span-3">
      <!-- Title container will render only the first h1 -->
      <div class="title-container">
        <h1>
          <TitleRenderer />
        </h1>
      </div> 
       <!-- Content container will render everything else -->
      <div class="content-container two-cols">
        <!-- Top slot for content in the top row -->
        <div v-if="$slots.top" class="top-row" :class="alignment.t">
          <slot name="top" />
        </div>
        <div v-if="$slots.left" class="left-col" :class="alignment.l">
          <slot name="left" />
        </div>
        <div v-if="$slots.right" class="right-col" :class="alignment.r">
          <slot name="right" />
        </div>
        <div v-if="$slots.default" class="end-footer">
          <slot name="default" />
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


<style scoped>
.content-container.two-cols {
  display: grid;
  grid-template-columns: repeat(12, 1fr); /* 12 columns */
  grid-template-rows: auto 1fr auto; /* top row, main content, footer */
}

/* Top row spans full width */
.top-row {
  grid-area: 1 / 1 / 2 / span 12; /* full width in first row */
  margin-bottom: 1.5rem;
  display: flex;
  flex-direction: column;
}

.end-footer {
  grid-area: 3 / 1 / 4 / span 12; /* full width in third row */
  margin-bottom: 1rem;
}

.two-cols-footer .left-col {
  margin-right: 2rem;
  display: flex;
  flex-direction: column;
}

.two-cols-footer .right-col {
  display: flex;
  flex-direction: column;
}

.two-cols .left-col {
  margin-right: 2.5rem;
  display: flex;
  flex-direction: column;
}

.two-cols .right-col {
  margin-left: 2.5rem;
  display: flex;
  flex-direction: column;
}

/* Updated grid areas for main content row (now row 2) */
.two-cols-footer .left-col {
  grid-area: 2 / 1 / 3 / span v-bind(colwidth.l);
}

.two-cols-footer .right-col {
  grid-area: 2 / v-bind(colwidth.l + 1) / 3 / span v-bind(colwidth.r);
}

.two-cols .left-col {
  grid-area: 2 / 1 / 3 / span v-bind(colwidth.l);
}

.two-cols .right-col {
  grid-area: 2 / v-bind(colwidth.l + 1) / 3 / span v-bind(colwidth.r);
}
</style>
