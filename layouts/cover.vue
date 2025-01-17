<script setup lang="ts">
import { computed } from 'vue'
import { handleBackground, handleAuthor } from '../layoutHelper'
import Institutes from '../components/Institutes.vue';
import TitleRenderer from '#slidev/title-renderer'

const props = defineProps({
  authors: {
    type: Object as () => Record<string, string>,
    default: () => ({})
  },
  meeting: {
    type: String,
    default: '',
  },
  date: {
    type: String,
    default: new Date().toLocaleDateString(),
  },
})

// Process authors from dictionary to author name as key, and author affiliation as value
const authorList: string[] = props.authors.map(author => Object.keys(author)[0]);

const [authorsDict, instituteDict] = handleAuthor(props.authors);
console.log(authorsDict);
console.log(instituteDict);
</script>

<template>
  <div class="slidev-layout slidev-layout--vertlines">
    <img class="slidev-layout cover background" src = "../styles/cover_background_clean.svg" alt="My Happy SVG"/>
    <div class="slidev-layout cover">
      <div class="slidev-layout cover cover-container">
        <slot/>

        <div v-if="authorList.length">
          <p v-if="authorList.length > 1">
            <template v-for="(author, idx) in authorList">
              <span :class="{ 'underline': idx === 0 }">{{ author }}</span>
              <sup v-if="authorsDict[author].instituteNum.length > 0">
                <template v-for="(num, index) in authorsDict[author].instituteNum">
                  <span v-if="index > 0">, </span>
                  <span>{{ num }}</span>
                </template>
              </sup>
              <span v-if="(idx < authorList.length - 1 && authorList.length >= 3)">, </span>
              <span v-if="idx === authorList.length - 2"> and </span>
            </template>
          </p>
          <p v-else-if="authorList.length===1" >
            <template v-for="(author, idx) in authorList">
              <span>{{ author }}</span>
            </template>
          </p>
          <Institutes         
            :filled="false"
            :separator="false"
            x="l"
            :footnotes="instituteDict"
            :numbers="authorList.length>1"
            />
        </div>
 
      </div>

    </div>
    <Footer 
        :meeting="$slidev.configs.meeting"
        :slidenum=false>
    </Footer>
  </div>
</template>
