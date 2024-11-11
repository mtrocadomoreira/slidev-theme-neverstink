<script setup lang="ts">
import { computed } from 'vue'
import TitleRenderer from '#slidev/title-renderer'

const props = defineProps({
  sectionNumber: {
      type: Number,
  },
})
</script>

<template>
  <div class="slidev-layout slidev-layout--vertlines">
    <div class="slidev-layout section">
      <div class="container">
       <!-- Content container will render everything else -->
        <slot/>
      </div>
    </div>
    <Footer 
        :author="Object.keys($slidev.configs.authors[Object.keys($slidev.configs.authors)[0]])[0]" 
        :meeting="$slidev.configs.meeting"
        :date="$slidev.configs.date">
    </Footer>
  </div>
</template>
