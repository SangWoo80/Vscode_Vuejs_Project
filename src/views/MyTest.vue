<template>
  <div class="chapter">
    <ul class="list-group">
      <li v-for="(chapterNo, index) in chapterNumList" :key="index" class="list-group-item" style="text-align:left">
        Chapter {{chapterNo.chapter}} <button class="btn btn-primary"  v-on:click="clickChapter(chapterNo.chapter)">Choice Chapter</button> 
      </li>
    </ul>
    <vuejs2Chapter5 v-if="chapterNumValue==5"></vuejs2Chapter5>
    <vuejs2Chapter6 v-else-if="chapterNumValue==6" ></vuejs2Chapter6>   
    <h2 v-else>Chapter 를 선택해 주세요.</h2>
  </div>
</template>

<script>
import vuejs2Chapter5 from '@/components/Vuejs2_chapter5.vue'
import vuejs2Chapter6 from '@/components/Vuejs2_chapter6.vue'

export default {
  name: 'chapter',
  components: {
    vuejs2Chapter5,
    vuejs2Chapter6
  },
  data() {
    return {
      chapterNumValue:0,
      chapterNumList: [
        {chapter:5},
        {chapter:6}
      ]
    }    
  },
  methods: {
    clickChapter(choiceChapterNo) {
      console.log(">>>>> clickChapter <<<<<");

      console.log(choiceChapterNo);

      this.chapterNumValue = choiceChapterNo;
    }
  }
}
</script>