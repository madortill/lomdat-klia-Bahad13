<template>
    <page-layout @next="$emit('next')" @back="$emit('back')">
      
      <template #header-content>
        <h1 class="page-title">פקודת מעצר אדומה</h1>
      </template>
  
      <template #main-content>
        <div class="my-content">
         
  
          <div class="note-box arrow-left" style="top: 15vh; right: 8vw; max-width: 180px;">
            <p><strong>א.אני</strong></p>
            <p>בסעיף זה נציין את פרטי מאשר עצירתו של החשוד בדרגת סרן ומעלה</p>
          </div>
  
          <div class="note-box arrow-left" style="top: 30vh; right: 8vw; max-width: 180px;">
            <p>ב.מורה בזאת על מעצרו של בסעיף זה נציין את פרטי העצור</p>
          </div>
  
          <div class="note-box arrow-left" style="top: 55vh; right: 8vw; max-width: 180px;">
            <p><strong>ג.פרטי מבצע המעצר</strong></p>
            <p>בסעיף זה נציין את החייל אשר עצר את החשוד מד"צ / בלש</p>
          </div>
  
          <div class="note-box arrow-right" style="top: 45vh; left: 8vw; max-width: 180px;">
            <p><strong>סעיף 8:</strong></p>
            <p>בסעיף זה נציין את מועד עצירתו של העצור</p>
          </div>
  
          <div class="note-box arrow-right" style="top: 68vh; left: 8vw; max-width: 180px;">
            <p><strong>ד.אישור על קיום הליך שמיעת טענות המעצר</strong></p>
            <p>דרגת סרן ומעלה במידת ויש צורך בגביית אימרה</p>
          </div>
        </div>
      </template>
  
    </page-layout>
    <img src="@/assets/media/a4.webp" class="b-image" />
  </template>
<script>
import PageLayout from './PageLayout.vue';

export default {
  name: "RedOrderPage",
  components: { PageLayout },
  emits: ["next", "back"]
};

</script>

<style>
.page-title {
  font-family: "Karantina-Bold";
  font-size: 3rem;
}

/* מיכל ראשי יחסי שמאפשר למקם את כל האלמנטים באופן חופשי על המסך */
.my-content {
  position: relative;
  width: 100%;
  height: 80vh;
  bottom: 10vh;
}

.b-image {
  position: absolute;
  top: 8rem;
  left: 32vw; /* מרכז את הדף */
  width: 36%;
  height: 83%;
  object-fit: cover;
  z-index: 1;
}

/* --- עיצוב בסיסי לפתקים הקטנים --- */
.note-box {
  position: absolute;
  background-color: #fefad4; 
  border: 0.05rem solid #e1db9b;
  /* שימוש ב-rem ו-vw בשביל ריפוד רספונסיבי */
  padding: 0.5rem 1.5vw; 
  box-shadow: 0 0.25rem 0.5rem rgba(0, 0, 0, 0.05);
  z-index: 5;
  direction: rtl;
}

/* עיצוב הטקסט בתוך הפתק */
.note-box p {
  margin: 0 0 0.25rem 0;
  font-family: "Karantina-Light", sans-serif; 
  font-size: 1.5rem; 
  line-height: 1.1;
  color: #333;
}
.note-box p:last-child {
  margin-bottom: 0;
}

/* --- הבסיס המשותף לקו ולראש החץ --- */
.note-box::before,
.note-box::after {
  content: '';
  position: absolute;
  top: 50%;
  display: block;
}

/* =============================================
   1. פתקים בצד שמאל (החץ פונה ימינה לכיוון הדף)
   ============================================= */

/* הקו הישר השחור */
.note-box.arrow-right::before {
  /* מבוסס vw - מתארך ומתקצר לפי גודל המסך */
  right: -3vw;          
  width: 3vw;           
  height: 0.2vh; /* עובי הקו מבוסס גובה מסך */
  background-color: #000;
  transform: translateY(-50%);
}

/* ראש החץ השחור (המשולש) */
.note-box.arrow-right::after {
  /* ממוקם בדיוק ברוחב הקו פלוס חריגה קטנה ב-vw */
  right: calc(-3vw - 0.6vw); 
  transform: translateY(-50%);
  border-style: solid;
  /* שימוש ב-vw לרוחב וגובה המשולש לשמירה על פרופורציה */
  border-width: 0.6vh 0 0.6vh 0.8vw; 
  border-color: transparent transparent transparent #000; 
}

/* =============================================
   2. פתקים בצד ימין (החץ פונה שמאלה לכיוון הדף)
   ============================================= */

/* הקו הישר השחור */
.note-box.arrow-left::before {
  left: -3vw;           
  width: 3vw;
  height: 0.2vh;
  background-color: #000;
  transform: translateY(-50%);
}

/* ראש החץ השחור (המשולש) */
.note-box.arrow-left::after {
  left: calc(-3vw - 0.6vw); 
  transform: translateY(-50%);
  border-style: solid;
  border-width: 0.6vh 0.8vw 0.6vh 0; 
  border-color: transparent #000 transparent transparent; 
}
</style>