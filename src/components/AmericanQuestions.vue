<template>
    <div class="question-box">
      <h2 class="question-title">{{ currentQuestion?.title }}</h2>
      
      <div class="answers-container">
        <div class="row-ques">
          <button
            v-for="id in [1, 2]"
            :key="id"
            :disabled="isSolved"
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
            :disabled="isSolved"
            @click="checkAnswer(id)"
            :class="['answer-btn', getButtonClass(id)]"
          >
            {{ currentQuestion[`ans${id}`] }}
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

  emits: ["solved"],

  data() {
    return {
      selectedAnswers: [],
      isSolved: false,
      questionsData: data.questions
    };
  },

  computed: {
    currentQuestion() {
      return this.questionsData[this.numQues] || {};
    }
  },

  watch: {
    numQues() {
      this.selectedAnswers = [];
      this.isSolved = false;
    }
  },

  methods: {
    checkAnswer(answerId) {
      if (this.selectedAnswers.includes(answerId) || this.isSolved) return;

      this.selectedAnswers.push(answerId);

      const isCorrect =
        String(answerId) === String(this.currentQuestion.correctAnswer);

      if (isCorrect) {
        this.isSolved = true;
        this.$emit("solved");
      }
    },

    getButtonClass(id) {
      if (!this.selectedAnswers.includes(id)) return '';
      return id === this.currentQuestion.correctAnswer ? 'correct' : 'wrong';
    }
  }
};
</script>
  
  <style scoped>
  /* עיצוב הריבוע הלבן המרכזי בהתאם לתמונה שלך */
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
  
  /* עיצוב כפתורי התשובות הניטרליים (צהבהב בהיר כמו בעיצוב) */
  .answer-btn {
    flex: 1;
    max-width: 18rem;
    height: 5rem;
    background-color: #fefbe6; 
    border: 1px solid #dcd9bc;
    border-radius: 1.2rem;
    cursor: pointer;
    font-size: 1.2rem;
    transition: background-color 0.2s ease, border-color 0.2s ease;
  }
  
  /* מצבי צבע דינמיים */
  .answer-btn.correct {
    background-color: #5eff8b !important; /* ירוק זרחני בהיר כמו בתמונה */
    border-color: #4cd473 !important;
    color: #000000;
  }
  
  .answer-btn.wrong {
    background-color: #ff6b6b !important; /* אדום */
    border-color: #e04d4d !important;
    color: #ffffff;
  }
  
  /* במצב שהשאלה פתורה, כפתורים שלא נלחצו יאבדו את ה-pointer */
  .answer-btn:disabled {
    cursor: not-allowed;
  }
  </style>