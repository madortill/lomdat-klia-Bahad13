<!-- <template>
  <page-layout @next="$emit('next')" @back="$emit('back')">
    <template #main-content>
      <div class="four">
        <img src="@/assets/media/Group10.svg" class="f-img">
        <img src="@/assets/media/Group11.svg" class="f-img">
        <img src="@/assets/media/Group12.svg" class="f-img">
        <img src="@/assets/media/Group13.svg" class="f-img">
      </div>
    </template>
  </page-layout>
</template>

<script>
import PageLayout from './PageLayout.vue'
export default {
  name: "FoldersPage",
  components: { PageLayout },
  emits: ["next", "back"]
}
</script>

<style scoped>
.four {
  width: 80vw;
  height: 78vh;
  
  
  /* הגדרת הגריד ל-2 עמודות ו-2 שורות */
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
  
  /* ללא רווחים בכלל */
 
}

.f-img {
  width: 100%;
  height: 100%;
   display: block; /* מונע רווחים לבנים מיותרים בתחתית האלמנט */
  
  /* בחר לפי הצורך שלך: */
  object-fit: cover; /* ימלא את כל הריבוע (עלול לחתוך מעט מהצדדים של ה-SVG) */
  /* object-fit: fill; */ /* ימתח את התמונה בדיוק לגודל הריבוע (עלול לעוות אותה מעט) */
}
</style> -->
<template>
  <page-layout @next="$emit('next')" @back="$emit('back')">
    <template #main-content>
      <div class="four">
        <button 
          v-for="(folder, index) in folders" 
          :key="index"
          class="folder-btn" 
          @click="openPopup(folder)"
        >
          <img :src="folder.icon" class="f-img" :alt="folder.altText">
        </button>
      </div>

      <div v-if="isPopupOpen && activeFolder" class="popup-overlay">
  
  <div class="popup-content" @click.stop>
    
    <button class="close-btn" @click="closePopup">&times;</button>
    
    <h2 class="popup-title">{{ activeFolder.title }}</h2>
    
    <div class="forms-grid">
      <img 
        v-for="(imgSrc, imgIndex) in activeFolder.images" 
        :key="imgIndex"
        :src="imgSrc" 
        class="form-img" 
        alt="טופס"
      >
    </div>
  </div>
</div>
    </template>
  </page-layout>
</template>

<script>
import PageLayout from './PageLayout.vue'

// ייבוא האייקונים של התיקיות
import folderImg1 from '@/assets/media/Group10.svg'
import folderImg2 from '@/assets/media/Group11.svg'
import folderImg3 from '@/assets/media/Group12.svg'
import folderImg4 from '@/assets/media/Group13.svg'

import sayImg from '@/assets/media/arik/say.png'
import moveDepositFileImg from '@/assets/media/arik/moveDepositFile.png'
import complaintsImg from '@/assets/media/arik/complaints.png'
import pdArrestImg from '@/assets/media/arik/p+dArrest.png'
import idDepositImg from '@/assets/media/arik/id+deposit.png'

import idDataImg from '@/assets/media/mishtamet/id+data.png'
import sayHear from '@/assets/media/mishtamet/say+hear.png'
import deposit from '@/assets/media/mishtamet/deposit.png'

import law from '@/assets/media/havosh/law.png'
import health from '@/assets/media/havosh/health.png'
import moveFile from '@/assets/media/havosh/moveFile.png'
import identifyDeposit from '@/assets/media/havosh/identifyDeposit.png'

import id from '@/assets/media/id.png'



export default {
  name: "FoldersPage",
  components: { PageLayout },
  emits: ["next", "back"],
  data() {
    return {
      isPopupOpen: false,
      activeFolder: null, // ישמור את התיקייה שנלחצה כרגע
      
      // מערך המידע של התיקיות (שני את הכותרות והנתיבים לפי הצורך!)
      folders: [
        {
          title: "העברת משתמט" ,
          icon: folderImg1,
          altText: "תיקייה 1",
          images: [moveDepositFileImg, pdArrestImg, idDataImg, sayHear, deposit]
        },
        {
          title: "  העברת עריק",
          icon: folderImg2,
          altText: "תיקייה 2",
          images: [sayImg, moveDepositFileImg, complaintsImg, pdArrestImg, idDepositImg]
        },
        {
          title: "קליטת על''מ",
          icon: folderImg3,
          altText: "תיקייה 3",
          images: [pdArrestImg, id]
        },
        {
          title: "העברת חבוש",
          icon: folderImg4,
          altText: "תיקייה 4",
          images: [complaintsImg, law, health, moveFile, identifyDeposit  ]
        }
      ]
    }
  },
  methods: {
    openPopup(folder) {
      this.activeFolder = folder; // מעדכן איזה מידע להציג בפופ-אפ
      this.isPopupOpen = true;
    },
    closePopup() {
      this.isPopupOpen = false;
      this.activeFolder = null;
    }
  }
}
</script>

<style scoped>
/* עיצוב התיקיות והגריד הראשי */
.four {
  width: 80rem;
  height: 44rem; 
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
}

.folder-btn {
  background: none;
  border: none;
  padding: 0;
  cursor: pointer;
}

.f-img {
  width: 80%;
  height: 90%;
  display: block;
  object-fit: cover;
}

/* --- עיצוב הפופ-אפ (Modal) --- */

.popup-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.4);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 9999;
}

.popup-content {
  background-color: #fefbe6;
  padding: 4vh 3vw;
  border-radius: 0.5rem;
  width: 85vw; /* הגדלנו מעט את רוחב הפופ אפ */
  height: 75vh; /* הגדלנו את גובה הפופ אפ מ-60vh ל-75vh כדי לתת מקום לתמונות הגדולות */
  max-width: 55rem; /* הגדלנו את המקסימום מ-45rem */
  box-shadow: 0 0.5vh 2vh rgba(0, 0, 0, 0.15);
  position: relative;
  text-align: center;
  
  display: flex;
  flex-direction: column;
  justify-content: space-between; 
}

.close-btn {
  position: absolute;
  top: 2vh;
  right: 2.5vw;
  background: none;
  border: none;
  font-size: 2.5rem;
  cursor: pointer;
  font-weight: bold;
  color: #000;
  line-height: 1;
  height: 2rem;
}

.popup-title {
  font-family: "Karantina-bold";
  font-size: 7rem;
  margin-top: 0;
  margin-bottom: 1.5vh;
}

/* סידור הטפסים */
.forms-grid {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  row-gap: 3vh; /* הגדלנו מרווחים */
  column-gap: 2.5vw; 
  justify-items: center;
  align-items: center;
  flex-grow: 1;
}

/* הגדלת התמונות בפופ-אפ */
.form-img {
  width: 120%; /* הגדלה מ-100% כדי שיקבלו נפח גדול יותר */
  max-width: 32rem; /* הגדלה מ-25rem */
  height: auto;
  object-fit: contain;
}

/* סידור גמיש: ממרכז אוטומטית לפי כמות התמונות */
.forms-grid .form-img:nth-child(1) { grid-column: span 2; }
.forms-grid .form-img:nth-child(2) { grid-column: span 2; }
.forms-grid .form-img:nth-child(3) { grid-column: span 2; }

/* 2 הטפסים האחרונים (אם קיימים) מקבלים היסט למרכז */
.forms-grid .form-img:nth-child(4) { grid-column: 2 / span 2; }
.forms-grid .form-img:nth-child(5) { grid-column: 4 / span 2; }
</style>