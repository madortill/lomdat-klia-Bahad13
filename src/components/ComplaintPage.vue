<template>
    <PageLayout 
      :isNextDisabled="!doneReading" 
      @next="goToNextPage" 
      @back="goToPreviousPage"
    >
      <template #header-content>
        <h1 class="page-title">לומדת הנדסה רפואית</h1>
      </template>
  
      <template #main-content>
        <Book v-model:doneReading="doneReading" />
      </template>
    </PageLayout>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import PageLayout from './PageLayout.vue';
  import Book from './Book.vue';
  
  // המשתנה שיקבע אם הגענו לעמוד האחרון
  const doneReading = ref(false);
  
  const goToNextPage = () => {
    console.log("עוברים לעמוד הבא בלומדה!");
    // כאן הלוגיקה שלך למעבר מסך (למשל vue-router)
  };
  
  const goToPreviousPage = () => {
    console.log("חוזרים מסך אחורה");
  };
  </script>
  
  <style>
  .page-title {
    color: white;
    font-family: sans-serif;
    font-size: 1.5rem;
    margin: 0;
  }
  </style>