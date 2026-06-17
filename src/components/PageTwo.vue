<template>
    <page-layout @next="$emit('next')" @back="$emit('back')">
      
      <template #header-content>
        <h1 class="page-title">נושא שיעור: מערכות רכב</h1>
      </template>
  
      <template #main-content>
        <div class="my-content">
          <p>כאן יבוא התוכן המרכזי, הגרפיקות המודולריות או השאלות שלך...</p>
        </div>
      </template>
  
    </page-layout>
  </template>
  
  <script>
  import PageLayout from './PageLayout.vue';
  
  export default {
    name: "Page2",
    components: { PageLayout },
    emits: ["next", "back"]
  };
  </script>
  
  <style scoped>
  .page-title {
    font-family: "Karantina-Bold";
    font-size: 2.5rem;
    color: #ffffff;
  }
  
  .my-content {
    font-family: "Assistant-Regular";
    font-size: 1.5rem;
    color: #ffffff;
    text-align: center;
  }
  </style>