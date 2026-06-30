<template>
    <page-layout @next="$emit('next')" @back="$emit('back')">
        <template #main-content>
          <div class="soldier-layout">
    
    <div class="speech-bubble-c">
      <h3>   טופס 630</h3>
      <p >     טופס 630 הוא טופס שקצין שיפוט ממלא כאשר הוא שופט חייל לדין משמעתי. כאשר חייל נשפט בטופס זה הוא יכול לקבל גם עונש מחבוש , עבורנו זו אסמכתא המהווה הוכחה לכך שהחיייל אכן נשפט לכלא ושכליאתו חוקית.</p>
      <p>    בנוסף בטופס זה ניתן לראות על מה נשפט החייל ולכמה זמן , דבר שישמש אותנו על מנת להכניס את פרטיו למערכת "כחול אדום".</p>
     
    </div>

    <div class="soldier">
      <img src="@/assets/media\Gemini_Generated_Image_ytg63cytg63cytg6.svg" class="s-img" alt="soldier" />
    </div>

  </div>
  

        </template>
        
    </page-layout>
    <!-- <img src="@/assets/media/Gemini_Generated_Image_ytg63cytg63cytg6 1.svg"/> -->
  </template>
  
  <script>
  import PageLayout from './PageLayout.vue';
  
  export default {
    name: "Deposit",
    components: { PageLayout },
    emits: ["next", "back"]
  }
  </script>
  
  <style scoped>
  /* אלמנט עוטף חדש שמחבר ביניהם */
  .soldier-layout {
  position: relative;
  display: inline-block; 
  left: 20vw;
  bottom: 10vh;
}

/* --- החייל (במיקום המקורי שלך) --- */
.soldier {
  position: relative;
  right: -1vw;
  top: 30vh;
  width: 100%;
  height: 100%;
}

.s-img {
  object-fit: contain;
  width: 50vw;
  height: 50vh;
}

/* --- בועת הדיבור (במיקום ובגודל המקורי שלך) --- */
.speech-bubble-c {
  position: absolute;
  top: -8vh; 
  left: -15vw; 
  
  background: rgba(239, 241, 246, 0.95); 
  color: #000; 
  
  padding: 30px 40px;      
  border-radius: 40px;     
  width: 50vw;             
  max-width: 650px;        
  
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.08);
  z-index: 10; 
  text-align: center;      
}

/* עיצוב הכותרת */
.speech-bubble-c h3 {
  margin: 0 0 20px 0;      
  font-family: "Karantina-Bold", sans-serif;
  font-size: 3.5rem;       
  font-weight: bold;
  direction: rtl;
}

/* עיצוב פסקאות הטקסט */
.speech-bubble-c p {
  margin: 5px 0;
  font-family: "Karantina-Light", sans-serif;
  font-size: 2.5rem;       
  line-height: 1.4;        
  direction: rtl;
}

/* ה"זנב" המקורי שלך */
.speech-bubble-c::after {
  content: '';
  position: absolute;
  bottom: -25px;           
  right: 60px;             
  
  border-width: 25px 20px 0 20px; 
  border-style: solid;
  border-color: rgba(239, 241, 246, 0.95) transparent transparent transparent;
  display: block;
  width: 0;
}

/* ==========================================================================
   נקודת השבירה: ברגע שהמסך קטן ממחשב (מתחת ל-1024px - כולל טאבלטים ומובייל)
   ========================================================================== */
   @media (max-width: 1388px) {
  /* הופך את המבנה לאנכי וממרכז את האלמנטים */
  .soldier-layout {
    display: flex;
    flex-direction: column; 
    align-items: center;
    justify-content: center;
    left: 0;        /* מאפס מיקומי דסקטופ */
    bottom: 0;      /* מאפס מיקומי דסקטופ */
    width: 90vw; 
    height: 48vh;   /* תופס את רוב רוחב המסך */
    margin: 0 auto; /* ממרכז את הכל במסך */
    padding-top: 4vh;
  }

  /* בועת הדיבור הופכת לחלק מהזרימה ולא מרחפת */
  .speech-bubble-c {
    position: relative; 
    top: 0;             
    left: 0;            
    width: 100%;        /* מנצלת את רוב רוחב המסך הקיים */
    max-width: none;
    padding: 25px 30px; 
    border-radius: 30px;
  }

  /* החייל יורד מתחת לבועה ומקבל את הרווח הרספונסיבי המבוקש */
  .soldier {
    position: relative;
    top: 0;        
    right: 0;      
    
    /* --- המאפיין שאחראי על הרווח המדויק ביניהם --- */
    margin-top: 3rem; 
    
    display: flex;
    justify-content: center;
    width: 100%;
  }

  /* התאמת גודל תמונת החייל למסכים קטנים יותר */
  .s-img {
    width: 60vw; 
    height: auto;
  }

  /* ממרכז את הזנב בתחתית הבועה שיצביע ישירות למטה אל החייל */
  .speech-bubble-c::after {
    right: auto;
    left: 50%;
    transform: translateX(-50%);
    bottom: -20px;
    border-width: 20px 15px 0 15px;
    border-color: rgba(239, 241, 246, 0.95) transparent transparent transparent;
  }
}
</style>