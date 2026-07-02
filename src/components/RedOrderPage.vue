<!-- <template>
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
  top: 7rem;
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
</style> -->
<template>
  <PageLayout :isNextDisabled="!allHotspotsClicked" @next="$emit('next')" @back="$emit('back')">
    <template #main-content>
      <div class="interactive-center-container">
        
        <!-- הטופס ממורכז לחלוטין במסך -->
        <div class="form-wrapper-r">
          <img src="@/assets/media/files/redorder.jpeg" alt="Form" class="form-image" />
          
          <!-- נקודה חמה 1: לשונית נפתחת משמאל (tooltip-left) -->
          <div 
            class="hotspot" 
            :class="{ 'clicked': clickedHotspots.includes(1), 'active': activeTab === 1 }"
            style="top: 17%; left: 20%; width: 58%; height: 6%;" 
            @click="handleHotspotClick(1)"
          >
            <!-- הלשונית הקטנה של נקודה 1 -->
            <div class="tooltip-box tooltip-left" v-if="activeTab === 1">
              <h3>אני </h3>
              <p>    בסעיף זה נציין את פרטי מאשר עצירתו של החשוד בדרגת סרן ומעלה </p>
            </div>
          </div>

          <!-- נקודה חמה 2: לשונית נפתחת מימין (tooltip-right) -->
          <div 
            class="hotspot" 
            :class="{ 'clicked': clickedHotspots.includes(2), 'active': activeTab === 2 }"
            style="top: 25%; left: 20%; width: 58%; height: 6%;" 
            @click="handleHotspotClick(2)"
          >
            <!-- הלשונית הקטנה של נקודה 2 -->
            <div class="tooltip-box tooltip-right" v-if="activeTab === 2">
              <h3>מורה בזאת על מעצרו של: </h3>
              <p>    בסעיף זה נציין את פרטי העצור </p>
            </div>
          </div>
         
          <div 
            class="hotspot" 
            :class="{ 'clicked': clickedHotspots.includes(3), 'active': activeTab === 3 }"
            style="top: 51%; left: 20%; width: 59%; height: 4%;" 
            @click="handleHotspotClick(3)"
          >
            <!-- הלשונית הקטנה של נקודה 2 -->
            <div class="tooltip-box tooltip-left" v-if="activeTab === 3">
              <h3>    סעיף 8:</h3>
              <p>    בסעיף זה נציין את מועד עצירתו של העצור </p>
            </div>
          </div>
         
          <div 
            class="hotspot" 
            :class="{ 'clicked': clickedHotspots.includes(4), 'active': activeTab === 4 }"
            style="top: 56%; left: 20%; width: 58.5%; height: 8%;" 
            @click="handleHotspotClick(4)"
          >
            <!-- הלשונית הקטנה של נקודה 2 -->
            <div class="tooltip-box tooltip-right" v-if="activeTab === 4">
              <h3>   פרטי מבצע המעצר: </h3>
              <p>    בסעיף זה נציין את  החייל אשר עצר את החשוד מד"כ / בלש </p>
            </div>
          </div>
         
          <div 
            class="hotspot" 
            :class="{ 'clicked': clickedHotspots.includes(5), 'active': activeTab === 5 }"
            style="top: 79%; left: 20%; width: 58%; height: 6%;" 
            @click="handleHotspotClick(5)"
          >
            <!-- הלשונית הקטנה של נקודה 2 -->
            <div class="tooltip-box tooltip-left" v-if="activeTab === 5">
              <h3>    אישור על קיום הליך שמיעת טענות העצור:</h3>
              <p>       דרגת סרן ומעלה במידה ויש צורך בגביית אמרה     </p>
            </div>
          </div>
        </div>

        <!-- מד התקדמות צף קטן בתחתית המסך (אופציונלי, בשביל הנוחות) -->
        <div class="progress-floating-tag">
          נבדקו {{ clickedHotspots.length }} מתוך {{ totalHotspots }} אזורים
        </div>

      </div>
    </template>
  </PageLayout>
</template>

<script>
import PageLayout from './PageLayout.vue';

export default {
  name: "InteractiveFormPage",
  components: { PageLayout },
  emits: ["next", "back"],
  
  data() {
    return {
      activeTab: null,          // איזו לשונית פתוחה כרגע
      clickedHotspots: [],     // מערך של הריבועים שנלחצו
      totalHotspots: 5         // סך הכל ריבועים שצריך ללחוץ עליהם
    };
  },
  
  computed: {
    allHotspotsClicked() {
      return this.clickedHotspots.length === this.totalHotspots;
    }
  },
  
  methods: {
    handleHotspotClick(id) {
      // אם לוחצים על לשונית שכבר פתוחה - נסגור אותה (Toggle)
      if (this.activeTab === id) {
        this.activeTab = null;
      } else {
        this.activeTab = id;
      }
      
      // הוספה למערך הלחיצות לאישור כפתור הבא
      if (!this.clickedHotspots.includes(id)) {
        this.clickedHotspots.push(id);
      }
    }
  }
};
</script>

<style scoped>
/* מרחב ראשי - ממרכז את הטופס לחלוטין */
.interactive-center-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  position: relative;
}

/* קונטיינר הטופס */
.form-wrapper-r {
  position: relative; /* מאפשר לריבועים וללשוניות להתמקם לפי אחוזים מהתמונה */
  width: 65vw;
  height: 100vh;       /* גודל נוח שמשאיר מקום ללשוניות בצדדים */
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
  border-radius: 8px;
  background: white;
}

.form-image {
  width: 100%;
  height: 88vh;
  display: block;
}

/* הריבועים הלחיצים על הטופס */
.hotspot {
  position: absolute;
  background-color: rgba(241, 196, 15, 0.2);
  border: 2px dashed #f1c40f;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.hotspot:hover {
  background-color: rgba(241, 196, 15, 0.35);
}

.hotspot.clicked {
  border-color: #2ecc71;
  background-color: rgba(46, 204, 113, 0.1);
}

.hotspot.active {
  border-color: #3498db;
  background-color: rgba(52, 152, 219, 0.15);
}

/* 🌟 עיצוב בועת הלשונית הכללית */
.tooltip-box {
  position: absolute;
  background-color: #073799;
  color: #ffffff;
  padding: 1.2rem;
  border-radius: 8px;
  box-shadow: 0 6px 20px rgba(0,0,0,0.3);
  z-index: 100;
  width: 16vw;          /* רוחב הלשונית הקטנה */
  direction: rtl;
  cursor: default;     /* מניע סימון טקסט בטעות */
  pointer-events: auto; /* מאפשר לגעת בלשונית עצמה */
}

.tooltip-box h3 {
  color: #FFF2B4;
  font-size: 1.6rem;
  margin-bottom: 0.5rem;
  font-family: sans-serif;
}

.tooltip-box p {
  font-size: 1.2rem;
  line-height: 1.4;
  margin: 0;
  font-family: sans-serif;
}

/* 📍 מיקומים שונים ללשוניות בהתאם למחלקה (Class) */

/* פתיחה משמאל לריבוע */
.tooltip-left {
  top: 50%;
  right: 105%; /* זורק את הלשונית שמאלה מהריבוע */
  transform: translateY(-50%);
}

/* פתיחה מימין לריבוע */
.tooltip-right {
  top: 50%;
  left: 105%;  /* זורק את הלשונית ימינה מהריבוע */
  transform: translateY(-50%);
}

/* פתיחה מעל הריבוע */
.tooltip-top {
  bottom: 110%; /* זורק את הלשונית מעל הריבוע */
  left: 50%;
  transform: translateX(-50%);
}

/* פתיחה מתחת לריבוע */
.tooltip-bottom {
  top: 110%;  /* זורק את הלשונית מתחת לריבוע */
  left: 50%;
  transform: translateX(-50%);
}

/* תגית ההתקדמות הצפה */
.progress-floating-tag {
  margin-top: 2vh;
  background-color: rgba(7, 55, 153, 0.85);
  color: white;
  padding: 0.5rem 1.5rem;
  border-radius: 20px;
  font-size: 1.2rem;
  font-family: sans-serif;
}
</style>