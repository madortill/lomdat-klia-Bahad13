<template>
  <div class="question-box">
    <h2 class="question-title">
      {{ currentQuestion?.title }}
    </h2>

    <div class="answers-container">
      <div class="row-ques">
        <button
          v-for="id in [1, 2]"
          :key="id"
          :disabled="hasAnswered"
          @click="checkAnswer(id)"
          :class="['answer-btn', getButtonClass(id)]"
        >
          {{ currentQuestion[`ans${id}`] }}
        </button>
      </div>

      <div class="row-ques">
        <button
          v-for="id in [3, 4]"
          :key="id"
          :disabled="hasAnswered"
          @click="checkAnswer(id)"
          :class="['answer-btn', getButtonClass(id)]"
        >
          {{ currentQuestion[`ans${id}`] }}
        </button>
      </div>
    </div>

    <!-- פופאפ שמופיע רק לאחר תשובה שגויה -->
    <div
      v-if="showWrongPopup"
      class="popup-overlay"
    >
      <div class="wrong-popup">
        <h3 class="popup-title">
          תשובה לא נכונה
        </h3>

        <p class="popup-text">
          התשובה הנכונה היא:
        </p>

        <p class="correct-answer-text">
          {{ correctAnswerText }}
        </p>

        <button
          class="continue-btn"
          @click="continueAfterWrong"
        >
          המשך
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import data from "@/data.json";

export default {
  name: "AmericanQuestions",

  props: {
    numQues: {
      type: Number,
      required: true,
      default: 0
    }
  },

  emits: [
    "answered",
    "next-question"
  ],

  data() {
    return {
      selectedAnswer: null,
      hasAnswered: false,
      showWrongPopup: false,
      popupTimeout: null,
      questionsData: data.questions
    };
  },

  computed: {
    currentQuestion() {
      return this.questionsData[this.numQues] || {};
    },

    correctAnswerId() {
      return Number(
        this.currentQuestion.correctAnswer
      );
    },

    correctAnswerText() {
      return (
        this.currentQuestion[
          `ans${this.correctAnswerId}`
        ] || ""
      );
    }
  },

  watch: {
    numQues() {
      this.resetQuestion();
    }
  },

  beforeUnmount() {
    if (this.popupTimeout) {
      clearTimeout(this.popupTimeout);
    }
  },

  methods: {
    checkAnswer(answerId) {
      // אפשר לענות רק פעם אחת
      if (this.hasAnswered) return;

      this.selectedAnswer = answerId;
      this.hasAnswered = true;

      const isCorrect =
        Number(answerId) ===
        Number(this.currentQuestion.correctAnswer);

      // מעדכנים את העמוד הראשי
      // כדי שיוכל לספור את הציון
      this.$emit("answered", {
        isCorrect,
        questionIndex: this.numQues,
        selectedAnswer: answerId,
        correctAnswer: this.correctAnswerId
      });

      // אם התשובה שגויה:
      // קודם הכפתור נצבע באדום,
      // ורק אז נפתח הפופאפ
      if (!isCorrect) {
        this.popupTimeout = setTimeout(() => {
          this.showWrongPopup = true;
        }, 600);
      }
    },

    getButtonClass(id) {
      if (this.selectedAnswer === null) {
        return "";
      }

      // רק הכפתור שנלחץ משנה צבע
      if (id === this.selectedAnswer) {
        return (
          id === this.correctAnswerId
            ? "correct"
            : "wrong"
        );
      }

      return "";
    },

    continueAfterWrong() {
      this.showWrongPopup = false;

      this.$emit("next-question");
    },

    resetQuestion() {
      if (this.popupTimeout) {
        clearTimeout(this.popupTimeout);
        this.popupTimeout = null;
      }

      this.selectedAnswer = null;
      this.hasAnswered = false;
      this.showWrongPopup = false;
    }
  }
};
</script>

<style scoped>
.question-box {
  background-color: #ffffff;
  border-radius: 1.5rem;
  padding: 3rem;

  width: 80vw;
  max-width: 45rem;

  box-shadow: 0 0.5vh 2vh rgba(0, 0, 0, 0.05);

  text-align: center;
  direction: rtl;
}

.question-title {
  font-family: "Karantina-bold", sans-serif;
  font-size: 4.5rem;

  margin-top: 0;
  margin-bottom: 2rem;
}

.answers-container {
  display: flex;
  flex-direction: column;

  gap: 1.5rem;
}

.row-ques {
  display: flex;
  justify-content: center;

  gap: 2rem;
}

.answer-btn {
  flex: 1;

  max-width: 18rem;
  height: 5.5rem;

  background-color: #fefbe6;

  border: 1px solid #dcd9bc;
  border-radius: 1.2rem;

  cursor: pointer;

  font-size: 1.2rem;

  transition:
    background-color 0.2s ease,
    border-color 0.2s ease,
    transform 0.2s ease;
}

.answer-btn:not(:disabled):hover {
  transform: scale(1.03);
}

/* תשובה נכונה */
.answer-btn.correct {
  background-color: #5eff8b;

  border-color: #4cd473;

  color: #000000;
}

/* תשובה שגויה */
.answer-btn.wrong {
  background-color: #ff6b6b;

  border-color: #e04d4d;

  color: #ffffff;
}

/*
  אחרי בחירה כל הכפתורים disabled,
  אבל אנחנו לא רוצים שהם יהפכו לאפורים
*/
.answer-btn:disabled {
  cursor: default;
  opacity: 1;
}

/* ---------------------- */
/* פופאפ תשובה שגויה */
/* ---------------------- */

.popup-overlay {
  position: fixed;

  inset: 0;

  z-index: 1000;

  display: flex;
  justify-content: center;
  align-items: center;

  background-color: rgba(0, 0, 0, 0.35);
}

.wrong-popup {
  width: min(90vw, 30rem);

  padding: 2.5rem 3rem;

  background-color: #ffffff;

  border-radius: 1.5rem;

  box-shadow:
    0 1rem 3rem rgba(0, 0, 0, 0.2);

  text-align: center;
  align-items: center;
  display: flex;
  flex-direction: column;

  direction: rtl;

  animation: popupIn 0.25s ease;
}

.popup-title {
  margin: 0 0 1rem;

  font-family: "Karantina-bold", sans-serif;

  font-size: 3rem;
}

.popup-text {
  margin: 0 0 0.5rem;

  font-size: 1.2rem;
}

.correct-answer-text {
  margin: 1rem 0 2rem;
  
  font-size: 1.5rem;
  font-weight: 700;
  
}

.continue-btn {
  width: 25vw;
  max-width: 13rem;
  height: 7vh;
  max-height: 4.5rem;
  background-color: #992211;
  border-radius: 5rem;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transition: transform 0.2s ease, background-color 0.2s ease;
  box-shadow: 0 0.5vh 1.5vh rgba(0, 0, 0, 0.15);
  font-family: "Karantina-light", sans-serif;
  font-size: 2.5rem;
  color: #ffffff;
  align-items: center;

  transition: transform 0.2s ease;
}

.continue-btn:hover {
  transform: scale(1.04);
}

@keyframes popupIn {
  from {
    opacity: 0;
    transform: scale(0.9);
  }

  to {
    opacity: 1;
    transform: scale(1);
  }
}
</style>