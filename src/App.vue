<template>
  <div id="app">
    <component 
      :is="currentPageName" 
      @next="nextPage" 
      @back="prevPage"
    />
  </div>
</template>

<script>
// מייבאים את עמוד הפתיחה ואת שאר העמודים (לדוגמה Page2)
import OpenPage from './components/OpenPage.vue';
import PageTwo from './components/PageTwo.vue';
import Importance from './components/Importance.vue';
import ShiftPage from './components/ShiftPage.vue';
import Deposit  from './components/Deposit.vue';
import Say from './components/Say.vue'; 
import SayPage from './components/SayPage.vue';
import RedOrderPage from './components/RedOrderPage.vue';
import Annexation from './components/Annexation.vue';
import AnnexationPage from './components/AnnexationPage.vue';
import Complaint from './components/Complaint.vue';
import ComplaintPage from './components/ComplaintPage.vue';
import FoldersPage from './components/FoldersPage.vue';
import Practice from './components/practice.vue';
import AmericanQuestionsPage from './components/AmericanQuestionsPage.vue';
import LastPage from './components/lastPage.vue';

// import ComplaintPage from './components/ComplaintPage.vue';

// import Page2 from './components/Page2.vue'; 

export default {
  name: "App",
  components: {
    OpenPage,
    PageTwo,
    Importance,
    ShiftPage,
    Deposit,
    Say,
    SayPage,
    RedOrderPage,
    Annexation,
    AnnexationPage,
    Complaint,
    ComplaintPage,
    FoldersPage,
    Practice,
    AmericanQuestionsPage, 
    LastPage
    // ComplaintPage,
    // Page2
  },
  data() {
    return {
      // מערך סדר העמודים - עמוד הפתיחה הוא הראשון
      pageOrder: [
        "OpenPage",
         "PageTwo",
         "Importance",
         "ShiftPage",
         "Deposit",
         "Say",
         "SayPage",
         "RedOrderPage",
         "Annexation",
         "AnnexationPage",
         "Complaint",
         "ComplaintPage",
         "FoldersPage",
         "Practice",
         "AmericanQuestionsPage",
         "LastPage"
        //  "ComplaintPage"
        // "Page3"
      ],
      currentPageIndex: 0
    };
  },
  computed: {
    currentPageName() {
      return this.pageOrder[this.currentPageIndex];
    }
  },
  methods: {
    nextPage() {
  if (this.currentPageIndex < this.pageOrder.length - 1) {
    this.currentPageIndex++;
  } else {
    // 🌟 כאן קורה הקסם: אם המשתמש הגיע לעמוד האחרון (LastPage) ולחץ, מחזירים אותו לאינדקס 0
    console.log("מאתחלים את הלומדה וחוזרים לעמוד הראשון!");
    this.currentPageIndex = 0;
  }
},
    prevPage() {
      if (this.currentPageIndex > 0) {
        this.currentPageIndex--;
      }
    }
  }
};
</script>

<style>
/* הגדרת הפונטים נשארת כאן ללא שינוי */
@font-face {
  font-family: "Karantina-Regular";
  src: url('./assets/fonts/Karantina-Regular.ttf');
}
@font-face {
  font-family: "Karantina-Light";
  src: url('./assets/fonts/Karantina-Light.ttf');
}
@font-face {
  font-family: "Karantina-Bold";
  src: url('./assets/fonts/Karantina-Bold.ttf');
}
@font-face {
  font-family: "Assistant-Regular";
  src: url('./assets/fonts/Assistant/Assistant-Regular.ttf');
}
@font-face {
  font-family: "Assistant-Bold";
  src: url('./assets/fonts/Assistant/Assistant-Bold.ttf');
}
@font-face {
  font-family: "ElonWiess";
  src: url('./assets/fonts/OHElonWiess-Regular.ttf');
}

* {
  margin: 0;
  padding: 0;
  box-box-sizing: border-box;
}

html, body, #app {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: #7bc0f2; 
  touch-action: manipulation;
}

html {
  font-size: calc(10px + 0.5vw);
}


</style>