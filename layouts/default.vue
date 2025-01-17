<script setup lang="ts">
import { computed } from 'vue'
import TitleRenderer from '#slidev/title-renderer'

const props = defineProps({
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
      <div class="content-container">
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
