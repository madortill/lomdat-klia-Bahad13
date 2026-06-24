<template>
    <page-layout @next="$emit('next')" @back="$emit('back')">
        <template #main-content>
          <div class="soldier-wrapper">
    
    <div class="speech-bubble">
      <h3>תעודת העברה של כלוא</h3>
      <p class="speech-p">טקסט טקסט טקסט טקסט טקסט</p>
      <p>טקסט טקסט טקסט טקסט טקסט</p>
    </div>

    <div class="soldier">
      <img src="@/assets/media\Gemini_Generated_Image_ytg63cytg63cytg6 1.svg" class="s-img" alt="soldier" />
    </div>

  </div>
  

        </template>
        
    </page-layout>
    <!-- <img src="@/assets/media/Gemini_Generated_Image_ytg63cytg63cytg6 1.svg"/> -->
  </template>
  
  <script>
  import PageLayout from './PageLayout.vue';
  
  export default {
    name: "ShiftPage",
    components: { PageLayout },
    emits: ["next", "back"]
  }
  </script>
  
  <style scoped>
  /* אלמנט עוטף חדש שמחבר ביניהם */
  .soldier-wrapper {
  position: relative;
  display: inline-block; 
  left: 20vw;
  bottom: 10vh;
}

.soldier {
  position: relative;
  
  right: 2.5vw;
  top: 30vh;
  width: 100%;
  height: 100%;
}

.s-img {
  object-fit: contain;
  width: 50vw;
  height: 50vh;
}

/* --- עיצוב בועת הדיבור המשופרת --- */
.speech-bubble {
  position: absolute;
  
  /* מיקום מרכזי וגבוה בהרבה מהחייל */
  top: -8vh; 
  left: -15vw; 
  
  /* צבע הרקע והטקסט המקוריים מהעיצוב שלך */
  background: rgba(239, 241, 246, 0.95); /* גוון בהיר/אפרפר נקי */
  color: #000; 
  
  /* הגדלת הבועה והתאמה למראה המלבני העגול מהתמונה */
  padding: 30px 40px;      
  border-radius: 40px;     
  width: 50vw;             /* רווח רחב כמו בתמונה */
  max-width: 650px;        
  
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.08);
  z-index: 10; 
  text-align: center;      /* מרכוס הטקסט בתוך הבועה */
}

/* עיצוב הכותרת המופרדת */
.speech-bubble h3 {
  margin: 0 0 20px 0;      /* מרווח תחתון שמפריד מהטקסט */
  font-family: "Karantina-Bold", sans-serif;
  font-size: 3.5rem;       /* כותרת גדולה ובולטת */
  font-weight: bold;
  direction: rtl;
}

/* עיצוב פסקאות הטקסט בתוך הבועה */
.speech-bubble p {
  margin: 5px 0;
  font-family: "Karantina-Light", sans-serif;
  font-size: 2.5rem;       
  line-height: 1.4;        
  direction: rtl;
}



/* ה"זנב" (אפטר) - ממוקם בפינה הימנית התחתונה כדי להצביע על החייל */
.speech-bubble::after {
  content: '';
  position: absolute;
  bottom: -25px;           /* דוחף את המשולש מתחת לבועה */
  right: 60px;             /* מיקום בצד ימין (מעל החייל שנמצא מימין) */
  
  /* יצירת משולש גדול וברור */
  border-width: 25px 20px 0 20px; 
  border-style: solid;
  border-color: rgba(239, 241, 246, 0.95) transparent transparent transparent;
  display: block;
  width: 0;
}
</style>