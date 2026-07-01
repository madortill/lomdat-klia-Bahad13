<template>
    <PageLayout :isNextDisabled="!allHotspotsClicked" @next="$emit('next')" @back="$emit('back')">
      <template #main-content>
        <div class="interactive-center-container">
          
          <!-- הטופס ממורכז לחלוטין במסך -->
          <div class="form-wrapper">
            <img src="@/assets/media/files/say.jpeg" alt="Form" class="form-image" />
            
            <!-- נקודה חמה 1: לשונית נפתחת משמאל (tooltip-left) -->
            <div 
              class="hotspot" 
              :class="{ 'clicked': clickedHotspots.includes(1), 'active': activeTab === 1 }"
              style="top: 21%; left: 8%; width: 85%; height: 6%;" 
              @click="handleHotspotClick(1)"
            >
              <!-- הלשונית הקטנה של נקודה 1 -->
              <div class="tooltip-box tooltip-left" v-if="activeTab === 1">
                <h3>פרטים </h3>
                <p>פרטיו של גובה האמרה  </p>
              </div>
            </div>
  
            <!-- נקודה חמה 2: לשונית נפתחת מימין (tooltip-right) -->
            <div 
              class="hotspot" 
              :class="{ 'clicked': clickedHotspots.includes(2), 'active': activeTab === 2 }"
              style="top: 79%; left: 7%; width: 88%; height: 8%;" 
              @click="handleHotspotClick(2)"
            >
              <!-- הלשונית הקטנה של נקודה 2 -->
              <div class="tooltip-box tooltip-right" v-if="activeTab === 2">
                <h3>חתימות </h3>
                <p>לא לשכוח להחתים במהלך כל האמרה</p>
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
        totalHotspots: 2         // סך הכל ריבועים שצריך ללחוץ עליהם
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
  .form-wrapper {
    position: relative; /* מאפשר לריבועים וללשוניות להתמקם לפי אחוזים מהתמונה */
    width: 38vw;        /* גודל נוח שמשאיר מקום ללשוניות בצדדים */
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