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
                <a :href="medicalPdf" target="_blank" rel="noopener noreferrer">
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
              class="page-img" 
            />
          </div>
        </div>
  
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted, onUnmounted, nextTick } from 'vue';
  import { PageFlip } from 'page-flip';
  
  // --- 1. כל ה-Imports חייבים להיות כאן בראש הקובץ ---
  import coverImg from '@/assets/media/pic.png';
  import page1Img from '@/assets/media/pic.png';
  import page2Img from '@/assets/media/pic.png';
  import page3Img from '@/assets/media/pic.png';
  import page4Img from '@/assets/media/pic.png';
  import page5Img from '@/assets/media/pic.png';
  import medicalPdf from '@/assets/media/pic.png';
  
  // --- 2. הגדרת ה-Props וה-Emits ---
  defineProps({
    showNextBtn: Boolean,
    doneReading: Boolean
  });
  
  const emit = defineEmits(['update:showNextBtn', 'update:doneReading']);
  
  // --- 3. משתנים ומערכים ---
  // מערך הדפים (בסדר הפוך עבור קריאה מימין לשמאל)
  const pages = [page5Img, page4Img, page3Img, page2Img, page1Img, coverImg];
  
  const bookContainer = ref(null);
  let pageFlipInstance = null;
  
  const dimensions = ref({ width: 350, height: 500 });
  const bookReady = ref(false);
  
  // --- 4. פונקציות וניהול רספונסיביות ---
  const handleResize = () => {
    if (window.innerWidth <= 530) {
      dimensions.value = { width: 210, height: 300 };
    } else if (window.innerWidth <= 600) {
      dimensions.value = { width: 250, height: 360 };
    } else {
      dimensions.value = { width: 350, height: 500 };
    }
    
    if (pageFlipInstance) {
      pageFlipInstance.updateFromHtml();
    }
  };
  
  // מאזין יחיד ומאוחד לפיכת דף
  const onPageFlip = (e) => {
    const currentPage = e.data;
    // עמוד 0 הוא העמוד האחרון בספר
    if (currentPage === 0) {
      emit('update:doneReading', true);
      emit('update:showNextBtn', true);
    } else {
      emit('update:doneReading', false);
      emit('update:showNextBtn', false);
    }
  };
  
  // --- 5. Lifecycle Hooks ---
  onMounted(async () => {
    handleResize();
    window.addEventListener('resize', handleResize);
  
    await nextTick();
  
    if (bookContainer.value) {
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
  
      pageFlipInstance.loadFromHTML(bookContainer.value.querySelectorAll('.page-wrapper'));
      pageFlipInstance.on('flip', onPageFlip);
  
      bookReady.value = true;
      pageFlipInstance.turnToPage(5);
    }
  });
  
  onUnmounted(() => {
    window.removeEventListener('resize', handleResize);
    if (pageFlipInstance) {
      pageFlipInstance.destroy();
    }
  });
  
  // פונקציות ה-Hover
  const handleMouseEnter = (e) => {
    e.target.style.fill = 'rgba(255, 255, 255, 0.1)';
  };
  const handleMouseLeave = (e) => {
    e.target.style.fill = 'transparent';
  };
  </script>
  
  <style scoped>
  .book.hidden {
    opacity: 0;
    visibility: hidden;
  }
  .book.visible {
    opacity: 1;
    visibility: visible;
    transition: opacity 0.3s ease;
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
    display: block;
  }
  </style>