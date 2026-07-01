<template>
    <div class="open-page-container">
      
      <img src="@/assets/media/background.svg" alt="background" class="bg-image" />
      <div class="open-symbols">
          <img src="@/assets/media/bahad13.png" class="bahad"/>
          <img src="@/assets/media/til.svg" class="til"/>
      </div>
      
      <div class="last-btn" @click="$emit('next')">
        <span class="last-btn-text">חזור אל תחילת הלומדה</span>
      </div>
  
      <div class="start-text">
        <h1 class="start-text-title">!!!סיימתם את הלומדה בהצלחה</h1>
        <p class="start-text-fill">סיימתם את הלומדה והצלחתם לענות על כל השאלות ומילאתם</p>
        <p class="start-text-fill">את התיקיות בטפסים כמבוקש</p>    
        <p class="start-text-fill">אם תרצו תוכלו לחזור לתחילת הלומדה </p>
  
      </div>
  
      <div class="about-wrapper">
    <div :class="['div-about', showAbout ? 'fade-in' : 'fade-out']">
      <template v-if="showAbout">
        <h3 class="list-text-about">מפתחת ראשית:</h3>
        <p class="list-text-about">רב"ט ירין חנה טובול</p>
  
        <h3 class="list-text-about">מומחית תוכן:</h3>
        <p class="list-text-about">סגן ג'ולי יצחק</p>
        
  
        <h3 class="list-text-about">רמ"ד טי"ל:</h3>
        <p class="list-text-about">סמ"ר קטיה מדבדב</p>
  
        <h3 class="list-text-about">גרסה:</h3>
        <p class="list-text-about">יולי 2026</p>
      </template>
    </div>
  
    <div class="aboutBtnContainer" @click="toggleAbout">
      <button class="about-btn">{{ infoSymbol }}</button>
    </div>
  </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "OpenPage",
    emits: ["next"],
    data() {
        return {
          showAbout: false,
          infoSymbol: "i"
        };
      },
    
      methods: {
        toggleAbout() {
          this.showAbout = !this.showAbout;
          this.infoSymbol = this.infoSymbol === "i" ? "x" : "i";
        },
      }
    };
  </script>
  
  <style scoped>
  /* הגדרות גלובליות לאיפוס - מוודא שהקונטיינר באמת תופס את כל המסך */
  .open-page-container {
    position: relative;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
    display: flex;
    justify-content: center; /* ממרכז אופקית */
    align-items: center;     /* ממרכז אנכית */
    padding: 20px;           /* מרווח ביטחון כדי שהלוח לא יידבק לקצוות במסכים קטנים מאוד */
    box-sizing: border-box;
  }
  
  .bg-image {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    z-index: 1;
  }
  
  .open-symbols {
    position: absolute; /* שינוי מ-relative ל-absolute */
    top: 2rem;          /* מרחק מהקצה העליון */
    left: 2rem;         /* מרחק מהקצה השמאלי */
    z-index: 2;
    display: flex;      /* מומלץ: כדי שהסמלים יעמדו יפה אחד ליד השני */
    gap: 1rem;          /* מרווח בין שני הסמלים */
    align-items: center;
  }
  
  /* אפשר להסיר את ה-width שהיה כאן קודם כדי שהם לא יידחסו */
  .bahad {
    width: 5rem;
  }
  
  .til {
    width: 5rem;
  }
  /* הקונטיינר הראשי בפינה הימנית התחתונה */
  .about-wrapper {
      position: absolute;
     left: 17vw;       
      TOP: 6.5vh;      
      display: flex;
      flex-direction: column;
      align-items: center;
      z-index: 10;      
  }
  
  .aboutBtnContainer {
      cursor: pointer;
      display: flex;
      justify-content: center;
      align-items: center;
  }
  
  /* כפתור העיגול */
  .about-btn {
      border: none;
      color: #FEECD8;
      background-color: #073799;
      border-radius: 50%;
      
      /* גודל קבוע לעיגול מושלם */
      width: 3.5rem;    
      height: 3.5rem;
      
      /* הגדרות פונט ומירכוז מושלם של ה-i וה-X */
      font-family: 'Times New Roman', Times, serif;
      font-size: 2rem;
      font-weight: bold;
      display: flex;
      justify-content: center; /* ממרכז אופקית */
      align-items: center;     /* ממרכז אנכית */
      line-height: 1;          /* מונע מהאותיות "לקפוץ" למטה */
      
      padding: 0;
      transition: transform 0.25s ease;
      cursor: pointer;
  }
  
  .about-btn:hover {
      transform: scale(1.15);
  }
  
  /* חלונית המידע */
  .div-about {
      position: absolute;
      bottom: 115%;     /* מרווח קטן מעל העיגול */
      color: #FFF2B4;
      width: 15rem;
      max-height: 60vh; 
      overflow-y: auto; 
      font-family: "assistant", sans-serif;
      background: #073799;
      border-radius: 1rem;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
      text-align: center;
      padding: 1rem 0;
      transition: opacity 0.3s ease, transform 0.3s ease;
      direction: rtl;   
  }
  
  .list-text-about {
      margin: 0.4rem 0;
      font-size: 1rem;
  }
  
  h3.list-text-about {
      font-weight: bold;
      margin-top: 0.8rem;
      color: #ffffff;   
  }
  
  /* אנימציות */
  .fade-in {
      opacity: 1;
      transform: translateY(0);
      pointer-events: auto;
  }
  
  .fade-out {
      opacity: 0;
      transform: translateY(10px); 
      pointer-events: none;         
  }
  
  /* לוח הטקסט המרכזי - רספונסיבי עם יחס קבוע */
  .start-text {
    position: relative;
    z-index: 2;
    margin-left: 2vw;
   
    background-color: rgba(255, 255, 255, 0.6); /* 60% לבן */
    border-radius: 5%;
    padding: 5vw; 
    font-family: "OH_ElonWiess" ;
  }
  
  .start-text-title {
    font-family: "ElonWiess";
    font-size: 5rem;
    text-align: center;
  }
  
  .start-text-fill {
    text-align: center;
    font-family: 'Rubik';
    font-weight: 300;
    font-style: italic;
    font-size: 2rem;
    margin-top: 1rem;
  }
  
  /* כפתור כניסה - ממוקם כעת באופן מוחלט ביחס לקונטיינר כדי שיהיה בצד שמאל */
  .last-btn {
    position: absolute;
    left: 15vw; /* מרחק קבוע מצד שמאל של המסך */
    z-index: 2;
    padding: 1.5vh 2vw;
    background-color: #992211;
    border-radius: 5rem;
    cursor: pointer;
    box-shadow: 0 0.5vh 2vh rgba(0, 0, 0, 0.3);
    transition: transform 0.2s ease;
  }
  
  .last-btn:hover {
    transform: scale(1.05);
  }
  
  /* טקסט בתוך הכפתור */
  .last-btn-text {
    font-family: "Karantina-light", sans-serif;
    font-size: 2.5rem;
    color: #ffffff;
  }
  </style>