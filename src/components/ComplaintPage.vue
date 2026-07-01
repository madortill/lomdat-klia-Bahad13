<template>
  <PageLayout 
    :isNextDisabled="!doneReading" 
    @next="goToNextPage" 
    @back="goToPreviousPage"
  >
    <template #header-content>
      <h1 class="page-title">טופס 630 </h1>
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
};

const goToPreviousPage = () => {
  console.log("חוזרים מסך אחורה");
};
</script>

<style scoped>
.page-title {
  color: BLACK;
  font-family: "Karantina-Bold" sans-serif;
  font-size: 4.5rem;
  margin: 0;
}
</style>