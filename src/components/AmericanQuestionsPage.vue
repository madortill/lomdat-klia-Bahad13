<template>
  <page-layout
    :show-back="false"
    :is-next-disabled="!isCurrentQuestionSolved"
    @next="handleNext"
  >
    <template #header-content>
      <!-- אם תרצי אפשר להוסיף כאן כותרת -->
    </template>

    <template #main-content>
      <american-questions
        :num-ques="currentQuesIndex"
        @answered="onQuestionAnswered"
        @next-question="handleWrongAnswerNext"
      />
    </template>
  </page-layout>
</template>

<script>
import PageLayout from "./PageLayout.vue";
import AmericanQuestions from "./AmericanQuestions.vue";

import data from "@/data.json";

export default {
  name: "AmericanQuestionsPage",

  components: {
    PageLayout,
    AmericanQuestions
  },

  emits: ["next"],

  data() {
    return {
      // השאלה שמוצגת כרגע
      currentQuesIndex: 0,

      /*
        true רק אם המשתמש ענה נכון.
        במקרה כזה כפתור הבא של PageLayout נפתח.
      */
      isCurrentQuestionSolved: false,

      // מספר התשובות הנכונות
      score: 0,

      questionsData: data.questions
    };
  },

  computed: {
    totalQuestions() {
      return this.questionsData.length;
    }
  },

  methods: {
    onQuestionAnswered(result) {
      console.log(
        "ANSWERED:",
        result
      );

      if (result.isCorrect) {
        // תשובה נכונה = נקודה
        this.score++;

        // פותחים את כפתור הבא
        this.isCurrentQuestionSolved = true;
      } else {
        /*
          תשובה שגויה:
          לא פותחים את כפתור הבא,
          כי המעבר יתבצע דרך
          הכפתור שבתוך הפופאפ.
        */
        this.isCurrentQuestionSolved = false;
      }

      console.log(
        `Score: ${this.score}/${this.totalQuestions}`
      );
    },

    /*
      לחיצה על "הבא" של PageLayout
      לאחר תשובה נכונה
    */
    handleNext() {
      this.goToNextQuestion();
    },

    /*
      לחיצה על "המשך"
      בפופאפ לאחר תשובה שגויה
    */
    handleWrongAnswerNext() {
      this.goToNextQuestion();
    },

    goToNextQuestion() {
      const isLastQuestion =
        this.currentQuesIndex >=
        this.totalQuestions - 1;

      if (!isLastQuestion) {
        this.currentQuesIndex++;

        // סוגרים שוב את כפתור הבא
        // בשביל השאלה החדשה
        this.isCurrentQuestionSolved = false;

        return;
      }

      // סיימנו את כל 11 השאלות
      this.finishQuiz();
    },

    finishQuiz() {
      console.log(
        `Quiz finished: ${this.score}/${this.totalQuestions}`
      );

      /*
        שמירת הציון ב-sessionStorage.

        לדוגמה:
        7 תשובות נכונות מתוך 11
        יישמר כ:
        americanQuestionsScore = "7"
        americanQuestionsTotal = "11"
      */

      sessionStorage.setItem(
        "americanQuestionsScore",
        String(this.score)
      );

      sessionStorage.setItem(
        "americanQuestionsTotal",
        String(this.totalQuestions)
      );

      // אופציונלי - גם אחוז
      const percentage = Math.round(
        (this.score / this.totalQuestions) * 100
      );

      sessionStorage.setItem(
        "americanQuestionsPercentage",
        String(percentage)
      );

      // ממשיכים לעמוד הבא בלומדה
      this.$emit("next");
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