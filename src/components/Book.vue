<template>
  <div :class="['book', bookReady ? 'visible' : 'hidden']">
    <div ref="bookContainer" class="flipbook-container">
      
      <div 
        v-for="(pageImg, index) in pages" 
        :key="index" 
        class="page-wrapper"
      >
        <div class="page">
          <div v-if="index === 1" class="page-with-overlay">
            <img :src="pageImg" :alt="`page ${index + 1}`" class="page-img" />
            
            <svg viewBox="-550 0 1200 900" class="hotpath-overlay">
              <a :href="pdfFile" target="_blank" rel="noopener noreferrer">
                <path
                  d="M 24.019531 7.605469 L 24.019531 370.375 L 621.5 370.375 L 621.5 7.605469 Z"
                  fill="transparent"
                  stroke="transparent"
                  style="cursor: pointer; pointer-events: all;"
                  @mouseenter="handleMouseEnter"
                  @mouseleave="handleMouseLeave"
                />
              </a>
            </svg>
          </div>

          <img 
            v-else 
            :src="pageImg" 
            :alt="`page ${index + 1}`" 
            :class="['page-img', index === 0 ? 'cover-page' : '']" 
          />
        </div>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, nextTick, computed } from 'vue';
import { PageFlip } from 'page-flip';

// --- הגדרת ה-Props וה-Emits ---
defineProps({
  doneReading: Boolean
});
const emit = defineEmits(['update:doneReading']);

// ==========================================
// 🛠️ כאן מחליפים את התמונות והקבצים בקלות!
// ==========================================
import coverImg from '@/assets/media/book/cover.png';
import p1 from '@/assets/media/book/pic.png';
import p2 from '@/assets/media/book/pic.png';
import p3 from '@/assets/media/book/pic.png';
import p4 from '@/assets/media/book/pic.png';
import p5 from '@/assets/media/book/pic.png';
import medicalPdf from '@/assets/media/book/pic.png';

const imagesList = {
  cover: coverImg,
  page1: p1,
  page2: p2,
  page3: p3,
  page4: p4,
  page5: p5,
  pdf: medicalPdf
};
// ==========================================

// יצירת מערך הדפים בסדר הפוך עבור קריאה מימין לשמאל (RTL)
const pages = computed(() => [
  imagesList.page5,
  imagesList.page4,
  imagesList.page3,
  imagesList.page2,
  imagesList.page1,
  imagesList.cover
]);

const pdfFile = computed(() => imagesList.pdf);

const bookContainer = ref(null);
let pageFlipInstance = null;

const dimensions = ref({ width: 350, height: 500 });
const bookReady = ref(false);

// חישוב המידות לפני האתחול
const updateDimensions = () => {
  if (window.innerWidth <= 530) {
    dimensions.value = { width: 210, height: 300 };
  } else if (window.innerWidth <= 600) {
    dimensions.value = { width: 250, height: 360 };
  } else {
    dimensions.value = { width: 350, height: 500 };
  }
};

const handleResize = () => {
  updateDimensions();
  if (pageFlipInstance) {
    // עדכון מידות דינמי ב-page-flip דורש לפעמים הגדרה מחדש או update
    pageFlipInstance.updateFromHtml();
  }
};

const onPageFlip = (e) => {
  const currentPage = e.data;
  // עמוד 0 הוא העמוד האחרון בספר (העמוד הכי פנימי במערך ההפוך שלנו)
  if (currentPage === 0) {
    emit('update:doneReading', true);
  } else {
    emit('update:doneReading', false);
  }
};

onMounted(async () => {
  // 1. קודם כל נמדוד את המסך הנוכחי
  updateDimensions();
  window.addEventListener('resize', handleResize);

  // 2. נחכה שה-DOM יתעדכן עם ה-v-for
  await nextTick();

  if (bookContainer.value) {
    try {
      pageFlipInstance = new PageFlip(bookContainer.value, {
        width: dimensions.value.width,
        height: dimensions.value.height,
        minWidth: dimensions.value.width,
        minHeight: dimensions.value.height,
        maxWidth: dimensions.value.width,
        maxHeight: dimensions.value.height,
        size: 'fixed',
        drawShadow: false,
        showCover: window.innerWidth > 600,
        usePortrait: window.innerWidth <= 600,
        mobileScrollSupport: true
      });

      // טעינת הדפים מה-HTML המרונדר
      pageFlipInstance.loadFromHTML(bookContainer.value.querySelectorAll('.page-wrapper'));
      pageFlipInstance.on('flip', onPageFlip);

      bookReady.value = true;
      
      // התחלת הספר מהעמוד האחרון במערך (שהוא ה-Cover המקורי שלנו בגלל ה-RTL)
      pageFlipInstance.turnToPage(5);
    } catch (error) {
      console.error("שגיאה באתחול ה-PageFlip:", error);
    }
  }
});

onUnmounted(() => {
  window.removeEventListener('resize', handleResize);
  if (pageFlipInstance) {
    pageFlipInstance.destroy();
  }
});

const handleMouseEnter = (e) => {
  e.target.style.fill = 'rgba(255, 255, 255, 0.15)';
};
const handleMouseLeave = (e) => {
  e.target.style.fill = 'transparent';
};
</script>

<style scoped>
.book {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 20px auto;
}
.book.hidden {
  opacity: 0;
  visibility: hidden;
}
.book.visible {
  opacity: 1;
  visibility: visible;
  transition: opacity 0.3s ease;
}
.flipbook-container {
  box-shadow: 0 10px 30px rgba(0,0,0,0.15);
}
.page-wrapper {
  background-color: #fff;
}
.page {
  width: 100%;
  height: 100%;
  position: relative;
}
.page-with-overlay {
  position: relative;
  width: 100%;
  height: 100%;
}
.hotpath-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 10;
}
.page-img {
  width: 100%;
  height: 100%;
  object-fit: fill;
  display: block;
}
</style>