<template>
    <page-layout @next="$emit('next')" @back="$emit('back')">
      
      <!-- <template #header-content>
        <h1 class="page-title">נושא שיעור: מערכות רכב</h1>
      </template> -->
  
      <template #main-content>
        <div class="my-content">
  <h2> בלומדה זו נלמד את חשיבות אסמכתאות הכליאה</h2>
  <p>בכל חלק נלמד על חשיבות הטופס והשפעתו על המשך התהליך של העצור,</p>
  <p> נראה איך הוא נראה בפועל ויסומנו דגשים והסברים .</p> 
  <p>לאורך כל הלומדה יהיה סרגל ניווט שיראה את הנושא הנוכחי,</p>
<p>כמה עברתם ואת הנושאים הבאים .</p> 
<p>בסוף הלומדה יהיה תרגול על כל הטפסים והתאמתם לתיקייה הנכונה</p>
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
  /* .page-title {
    font-family: "Karantina-Bold";
    font-size: 2.5rem;
    color: #ffffff;
  } */
  
  .my-content {
  /* מבטיח שהפאדינג והבורדר כלולים בתוך הרוחב והגובה שהגדרת */
  box-sizing: border-box; 
  
  position: relative;
  z-index: 2;
  background-color:  rgba(239, 241, 246, 0.95); /* 60% לבן */
  
  /* החלפנו ל-px או rem כי 5% עלול לעוות את הפינות במסכים רחבים */
  border-radius: 15px; 
  
  /* פאדינג הגיוני שלא חונק את הטקסט */
  padding: 2rem; 
  
  /* הגדרת רוחב רספונסיבי: מקסימום 500 פיקסלים, אבל תופס 90% מהמסך במסכים קטנים */
  width: 100%;
  max-width: 50rem;
  
  /* מאפשר למלבן לגדול בצורה גמישה לפי כמות הטקסט (במקום גובה קבוע) */
  height: auto; 
  min-height: 30rem; 

  /* עיצוב טקסט */
  font-family: "Karantina-Light", sans-serif;
  color: black;
  text-align: center;
  
  /* מונע מהטקסט לצאת החוצה במקרה של מילים ארוכות במיוחד */
  overflow-wrap: break-word; 
  word-wrap: break-word;
  top: -1rem;
}

/* עיצוב פנימי לכותרת ולטקסט */
.my-content h2 {
  font-size: 3rem;
  margin-top: 0;
  margin-bottom: 1rem;
  font-family: 'Karantina-Bold';
}

.my-content p {
  font-size: 2.8rem;
  margin: 0;
  line-height: 1.5;
}
  </style>