<template>
    <page-layout 
      :show-back="false" 
      :is-next-disabled="!isCurrentQuestionSolved"
      @next="handleNext"
    >
      <template #header-content>
        <!-- <h1 class="page-main-title">תרגול מסכם</h1> -->
      </template>
  
      <template #main-content>

        <american-questions 
          :num-ques="currentQuesIndex" 
          @solved="onQuestionSolved" 
        />
      </template>
    </page-layout>
  </template>
  
  <script>
  import PageLayout from './PageLayout.vue';
  import AmericanQuestions from './AmericanQuestions.vue';
  import data from "@/data.json";
  
  export default {
    name: "AmericanQuestionsPage",
  
    components: { 
      PageLayout, 
      AmericanQuestions 
    },
  
    data() {
  return {
    currentQuesIndex: 0,
    isCurrentQuestionSolved: false,
    questionsData: data.questions
  };
},

computed: {
  totalQuestions() {
    return this.questionsData.length;
  }
},

methods: {

 onQuestionSolved() {
  console.log("SOLVED");
  this.isCurrentQuestionSolved = true;
},

  handleNext() {

console.log("NEXT", this.currentQuesIndex);

if (this.currentQuesIndex < this.questionsData.length - 1) {

  this.currentQuesIndex++;
  this.isCurrentQuestionSolved = false;

} else {

  console.log("סיימנו שאלות");
  this.$emit("next");

}
}
}
  };
  </script>
  
  <style scoped>
  .page-main-title {
    font-family: "Karantina-bold", sans-serif;
    font-size: 5rem;
    margin-bottom: 37rem;
    text-align: center;
  }
  </style>