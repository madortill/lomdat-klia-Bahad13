<template>
  <page-layout @next="$emit('next')" @back="$emit('back')">
    <template #main-content>
      <div class="soldier-layout">
        
        <div class="speech-bubble">
          <h3>חשיבות אסמכתאות הכליאה</h3>
          
          <p 
            v-for="(lineText, index) in typedLines" 
            :key="index"
          >
            <span v-html="lineText"></span>
          </p>
        </div>

        <div class="soldier">
          <img src="@/assets/media/Gemini_Generated_Image_ytg63cytg63cytg6.svg" class="s-img" alt="soldier" />
        </div>

      </div>
    </template>
  </page-layout>
</template>

<script>
import PageLayout from './PageLayout.vue';

export default {
  name: "ShiftPage",
  components: { PageLayout },
  emits: ["next", "back"],
  data() {
    return {
      // 1. המערך המקורי שלך - לא לגעת
      originalInfoArr: [
        "לכל חייל שנעצר / נכלא אנו מחויבים להיות בעלי אסמכתא המאשרת את עיכובו או מעצרו.",
        "אסמכתאות אלו הינן אישור בעל תוקף משפטי המאשר את החזקת החייל תחת משמורת חוקית.",
        "<strong>כמו כן, בלי כל המסמכים הנחוצים הכנסתו למעצר לא תתאפשר.</strong>"
      ],
      // 2. מערך ריק שיתמלא באותיות בזמן אמת
      typedLines: [],
      // הגדרות מהירות
      typeSpeed: 40,   // מהירות הקלדה (מילישניות לאות)
      lineDelay: 1000, // כמה זמן לחכות בין סיום שורה לתחילת השורה הבאה
    };
  },
  mounted() {
    // מפעיל את אפקט ההקלדה כשהקומפוננטה עולה
    this.startTypingEffect();
  },
  methods: {
    // הפונקציה המרכזית שמנהלת את אפקט ההקלדה האמיתי
    async startTypingEffect() {
      // 1. מאתחלים את המערך המוצג
      this.typedLines = this.originalInfoArr.map(() => "");

      // 2. לולאה על פני כל השורות במערך המקורי
      for (let i = 0; i < this.originalInfoArr.length; i++) {
        // ממתינים להקלדה של השורה הנוכחית
        await this.typeLine(i);
        // אם זו לא השורה האחרונה, מחכים קצת לפני הבאה
        if (i < this.originalInfoArr.length - 1) {
          await this.wait(this.lineDelay);
        }
      }
    },

    // פונקציית עזר המקלידה שורה בודדת (מחזירה Promise כדי שנוכל לחכות לסיומה)
    typeLine(lineIndex) {
      return new Promise((resolve) => {
        const fullText = this.originalInfoArr[lineIndex];
        let currentCharacterIndex = 0;

        // טיימר שרץ כל 40 מילישניות
        const interval = setInterval(() => {
          if (currentCharacterIndex < fullText.length) {
            // הוספת אות אחת למערך שמוצג במסך
            this.typedLines[lineIndex] += fullText[currentCharacterIndex];
            currentCharacterIndex++;
          } else {
            // סיימנו את השורה - מנקים את הטיימר ומסיימים את ה-Promise
            clearInterval(interval);
            resolve();
          }
        }, this.typeSpeed);
      });
    },

    // פונקציית עזר להמתנה פשוטה
    wait(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    }
  }
}
</script>

<style scoped>
/* --- אלמנט עוטף (הקונטיינר הראשי) --- */
.soldier-layout {
  position: relative;
  display: inline-block; 
  /* שימוש ב-margin במקום ערכי right/bottom קיצוניים תורם ליציבות הרספונסיבית */
  margin-right: 10vw;
  margin-top: 15vh; 
  right: -18vw;
}

/* --- החייל --- */
.soldier {
  position: relative;
  width: 100%;
  height: 100%;
  z-index: 1;
  bottom: -10vh;
  right: -10vw;
  
}

.s-img {
  object-fit: contain;
  width: 50vw;
  height: 50vh;
  max-width: 600px; /* תעודת ביטוח למסכים ענקיים */
}

/* --- בועת הדיבור: מוגבהת ורספונסיבית --- */
.speech-bubble {
  position: absolute;
  
  /* הגבהנו משמעותית את הבועה מעל ראש החייל */
  top: -28vh; 
  left: -18vw; 
  
  background: rgba(239, 241, 246, 0.95);
  color: #000; 
  
  padding: 30px 40px;      
  border-radius: 40px;     
  width: 50vw;             
  max-width: 650px;        
  
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.08);
  z-index: 10; 
  text-align: center;      
  direction: rtl;
  box-sizing: border-box; 
}

/* --- עיצוב הכותרת --- */
.speech-bubble h3 {
  margin: 0 0 20px 0;      
  font-family: "Karantina-Bold", sans-serif;
  font-size: clamp(2rem, 4vw, 3.5rem); /* גודל פונט רספונסיבי שקטן במסכים בינוניים */
  font-weight: bold;
  text-align: center;
}

/* --- עיצוב פסקאות הטקסט --- */
.speech-bubble p {
  margin: 5px 0;
  font-family: "Karantina-Light", sans-serif;
  font-size: clamp(1.4rem, 2.5vw, 2.5rem); /* פונט רספונסיבי */
  line-height: 1.4;        
  white-space: normal;     
  word-wrap: break-word; 
  display: block;
  text-align: center;
}

/* --- ה"זנב" המקורי --- */
.speech-bubble::after {
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
   התאמה רספונסיבית מלאה למובייל וטאבלטים (מסכים קטנים מ-768px)
   ========================================================================== */
@media (max-width: 768px) {
  .soldier-layout {
    display: flex;
    flex-direction: column; /* מסדר את הבועה והחייל אחד מעל השני באופן טבעי */
    align-items: center;
    margin: 0 auto;
    width: 90vw;
    padding-top: 2vh;
  }


  .soldier {
    right: 0;
    bottom: 0;
    margin-top: 2rem; /* יוצר מרווח בטוח מתחת לבועה */
    display: flex;
    justify-content: center;
  }

  .s-img {
    width: 65vw; /* מגדילים מעט את החייל במובייל כדי שיהיה ברור */
    height: auto;
  }

  .speech-bubble {
    position: relative; 
    top: 0; 
    left: 0; 
    width: 100%; /* תופס את רוב רוחב הקונטיינר במובייל */
    padding: 20px 25px; /* פאדינג מעט קומפקטי יותר למובייל */
    border-radius: 30px;
  }
  
  .speech-bubble::after {
    right: auto;
    left: 50%;
    transform: translateX(-50%);
  }
}
  </style>