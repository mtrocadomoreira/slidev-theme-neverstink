<script>
export default {
  props: {
    author: {
      type: String,
    },
    meeting: {
      type: String,
    },
    date: {
        type: Date,
    },
    slidenum: {
      default: true,
      type: Boolean,
    },
  }
}
</script>

<template>
  <div class="slidev-layout footer">
    <div id="logo">
      <img src="./images/cern-awake.png" width="120"> </img>
    </div>
    <div id="author-meeting">
      <span v-if="meeting && author">{{ author }} &nbsp; | &nbsp; {{ meeting }}</span>
      <span v-else>{{ author }} {{ meeting }}</span>
    </div>
    <div id="date-slide">
      <span class="flex-grow-1">{{date}}</span>
      <span v-if="slidenum"><SlideCurrentNo /></span>
    </div>
  </div>
</template>
