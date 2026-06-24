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
import RedOrderPage from './components/RedOrderPage.vue';
import FoldersPage from './components/FoldersPage.vue';
// import ComplaintPage from './components/ComplaintPage.vue';

// import Page2 from './components/Page2.vue'; 

export default {
  name: "App",
  components: {
    OpenPage,
    PageTwo,
    Importance,
    ShiftPage,
    RedOrderPage,
    FoldersPage,
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
         "RedOrderPage",
         "FoldersPage"
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
        console.log("הגעת לסוף הלומידה!");
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