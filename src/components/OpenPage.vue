<template>
  <div class="open-page-container">
    
    <img src="@/assets/media/background.svg" alt="background" class="bg-image" />
    
    <div class="start-btn" @click="$emit('next')">
      <span class="start-btn-text">התחל את הלומדה</span>
    </div>

    <div class="start-text">
      <h1 class="start-text-title">לומדת אסמכתאות </h1>
      <h1 class="start-text-title">כליאה</h1>
      <p class="start-text-fill">בית הספר למשטרה צבאית</p>

    </div>
  </div>
</template>

<script>
export default {
  name: "OpenPage",
  emits: ["next"]
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
}

/* כפתור כניסה - ממוקם כעת באופן מוחלט ביחס לקונטיינר כדי שיהיה בצד שמאל */
.start-btn {
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

.start-btn:hover {
  transform: scale(1.05);
}

/* טקסט בתוך הכפתור */
.start-btn-text {
  font-family: "Karantina-light", sans-serif;
  font-size: 2.5rem;
  color: #ffffff;
}
</style>