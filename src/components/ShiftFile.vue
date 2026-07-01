<template>
    <PageLayout :isNextDisabled="!allHotspotsClicked" @next="$emit('next')" @back="$emit('back')">
      <template #main-content>
        <div class="interactive-form-container">
          
          <!-- צד ימין: הטופס עם האזורים הלחיצים -->
          <div class="form-wrapper">
            <img src="@/assets/media/files/.jpeg" alt="Form" class="form-image" />
            
            <!-- נקודה חמה 1: לדוגמה - חתימה -->
            <div 
              class="hotspot" 
              :class="{ 'clicked': clickedHotspots.includes(1), 'active': activeTab === 1 }"
              style="top: 20%; left: 15%; width: 25%; height: 10%;" 
              @click="handleHotspotClick(1)"
            ></div>
  
            <!-- נקודה חמה 2: לדוגמה - תאריך -->
            <div 
              class="hotspot" 
              :class="{ 'clicked': clickedHotspots.includes(2), 'active': activeTab === 2 }"
              style="top: 45%; left: 60%; width: 30%; height: 8%;" 
              @click="handleHotspotClick(2)"
            ></div>
  
            <!-- נקודה חמה 3: לדוגמה - פרטים אישיים -->
            <div 
              class="hotspot" 
              :class="{ 'clicked': clickedHotspots.includes(3), 'active': activeTab === 3 }"
              style="top: 75%; left: 40%; width: 45%; height: 12%;" 
              @click="handleHotspotClick(3)"
            ></div>
          </div>
  
          <!-- צד שמאל: הלשונית הצידית שמציגה הסברים -->
          <div class="explanation-sidebar">
            <div v-if="activeTab === null" class="sidebar-placeholder">
              <p>לחצו על האזורים המודגשים בטופס כדי לקרוא את ההסברים</p>
            </div>
            
            <div v-else class="sidebar-content">
              <h3>{{ currentExplanation.title }}</h3>
              <p>{{ currentExplanation.text }}</p>
            </div>
            
            <!-- מד התקדמות קטן המראה כמה נשאר ללחוץ -->
            <div class="progress-text">
              נבדקו {{ clickedHotspots.length }} מתוך {{ totalHotspots }} אזורים
            </div>
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
        activeTab: null,          // איזה הסבר מוצג כרגע בלשונית
        clickedHotspots: [],     // מערך ששומר את האינדקסים של הריבועים שנלחצו כבר
        totalHotspots: 3,        // סך הכל אזורים שחובה ללחוץ עליהם קודם
        
        // מאגר המידע של ההסברים - את יכולה לערוך את הטקסטים כאן בקלות
        explanations: {
          1: { title: "אזור החתימה", text: "כאן נדרשת חתימת מפקד בדרגת רס\"ן ומעלה בלבד. שימו לב שלא ניתן לאשר את הטופס ללא חתימה זו." },
          2: { title: "תאריך התייצבות", text: "התאריך המופיע כאן חייב להיות תואם ליום פתיחת תיק הכליאה בפועל ולא יאוחר מ-24 שעות ממועד ההנפקה." },
          3: { title: "פרטי הכלוא", text: "ודאו שכל הפרטים האישיים (מספר אישי, שם מלא, ויחידה) מולאו בצורה קריאה ותקינה ללא מחיקות." }
        }
      };
    },
    
    computed: {
      // בודק האם המשתמש לחץ על כל האזורים הנדרשים
      allHotspotsClicked() {
        return this.clickedHotspots.length === this.totalHotspots;
      },
      // מחזיר את הכותרת והמלל של הלשונית הפעילה כרגע
      currentExplanation() {
        return this.explanations[this.activeTab] || { title: "", text: "" };
      }
    },
    
    methods: {
      handleHotspotClick(id) {
        this.activeTab = id; // מעדכן את הלשונית הצידית להציג את התוכן של הריבוע הזה
        
        // אם הריבוע הזה עדיין לא נמצא במערך הלחיצות, נוסיף אותו
        if (!this.clickedHotspots.includes(id)) {
          this.clickedHotspots.push(id);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  /* סידור העמוד: טופס מימין, לשונית משמאל */
  .interactive-form-container {
    display: flex;
    flex-direction: row-reverse; /* עבודה ב-RTL (ימין לשמאל) */
    align-items: flex-start;
    justify-content: center;
    gap: 4vw;
    width: 90vw;
    margin: 0 auto;
  }
  
  /* אזור הטופס */
  .form-wrapper {
    position: relative; /* קריטי עבור המיקום של ה-hotspots */
    width: 40vw;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
    border-radius: 8px;
    overflow: hidden;
  }
  
  .form-image {
    width: 100%;
    height: auto;
    display: block;
  }
  
  /* עיצוב הריבועים השקופים על הטופס */
  .hotspot {
    position: absolute;
    background-color: rgba(241, 196, 15, 0.2); /* צבע צהוב חלש ושקוף כברירת מחדל */
    border: 2px dashed #f1c40f;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.2s ease;
  }
  
  /* אפקט במעבר עכבר */
  .hotspot:hover {
    background-color: rgba(241, 196, 15, 0.4);
    transform: scale(1.02);
  }
  
  /* עיצוב ריבוע שכבר לחצו עליו */
  .hotspot.clicked {
    background-color: rgba(46, 204, 113, 0.15); /* הופך לירוק עדין */
    border-color: #2ecc71;
  }
  
  /* עיצוב הריבוע שנבחר כרגע ומציג את הלשונית שלו */
  .hotspot.active {
    background-color: rgba(52, 152, 219, 0.25); /* כחול בולט */
    border-color: #3498db;
    box-shadow: 0 0 10px rgba(52, 152, 219, 0.5);
  }
  
  /* הלשונית הצידית להסברים */
  .explanation-sidebar {
    width: 25vw;
    background-color: #ffffff;
    border-right: 6px solid #073799; /* קו קישוט כחול בצד */
    border-radius: 8px;
    padding: 2rem;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    min-height: 300px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    direction: rtl;
  }
  
  .sidebar-placeholder {
    color: #7f8c8d;
    font-size: 1.5rem;
    text-align: center;
    margin-top: 4rem;
    font-style: italic;
  }
  
  .sidebar-content h3 {
    color: #073799;
    font-size: 2.2rem;
    margin-bottom: 1rem;
    font-family: sans-serif;
  }
  
  .sidebar-content p {
    color: #2c3e50;
    font-size: 1.6rem;
    line-height: 1.5;
  }
  
  .progress-text {
    font-size: 1.2rem;
    color: #7f8c8d;
    text-align: left;
    border-top: 1px solid #ecf0f1;
    padding-top: 1rem;
    margin-top: 2rem;
  }
  </style>