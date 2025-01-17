<script setup lang="js">
import { Script } from 'vm';
import { computed } from 'vue'

const props = defineProps({
  side: {
    default: 'l',
  },
})

const side = computed(() => {
  if (props.side === 'left' || props.side === 'l') {
    return 'left'
  } else if (props.side === 'right' || props.side === 'r') {
    return 'right'
  } else {
    return 'error'
  }
})

</script>

<template>
    <div class="grid grid-cols-2 w-full h-full">
        <div class="w-100% h-100%">
            <iframe id="frame" class="w-full h-full" src=""></iframe>

        </div>
    </div>
</template>