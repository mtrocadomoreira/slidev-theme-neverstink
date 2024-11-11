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
  }
}
</script>

<template>
  <div class="slidev-layout footer">
    <div id="logo">
      <img src="./images/cern-awake.png" width="120"> </img>
    </div>
    <div id="author-meeting">
      <span>{{ author }}</span> 
      <span v-if="meeting">&nbsp; | &nbsp; {{ meeting }}</span>
    </div>
    <div id="date-slide">
      <span class="flex-grow-1">{{date}}</span>
      <span><SlideCurrentNo /></span>
    </div>
  </div>
</template>
