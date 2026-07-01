<template>
  <div class="page-layout">
    
    <header class="layout-header">
      <div class="header-right">
  <div v-if="showBack" class="back-btn" @click="goBack">
    <img src="@/assets/media/backBTN.svg" alt="back" class="back-btn-img" />
    <p class="back-btn-text">{{ backText }}</p>
  </div>
</div>

      <div class="header-center">
        <slot name="header-content"></slot>
      </div>

      <div class="header-left">
        <div class="symbols">
          <img src="@/assets/media/til.svg" alt="til" class="symbol-img til-logo" />
          <img src="@/assets/media/bahad13.png" alt="bahad13" class="symbol-img bahad-logo" />
        </div>
      </div>
    </header>

    <main class="layout-content">
      <slot name="main-content"></slot>
    </main>

    <footer class="layout-footer">
      <div 
  :class="['next-btn', { 'disabled': isNextDisabled }]" 
  @click="!isNextDisabled && nextPage()"
>
        <span class="next-btn-text">{{ nextText }}</span>
      </div>
    </footer>

  </div>
</template>

<script>
export default {
  name: "PageLayout",
  emits: ["next", "back"],
  props: {
    isNextDisabled: {
      type: Boolean,
      default: false
    },
    // ה-prop החדש
    showBack: {
      type: Boolean,
      default: true // כברירת מחדל תמיד מוצג
    }
  },
  data() {
    return {
      backText: "חזור",
      nextText: "הבא"
    };
  },
  methods: {
    nextPage() {
      // אם הכפתור חסום, אנחנו עוצרים ולא שולחים את האיוונט לאבא
      if (this.isNextDisabled) return;
      this.$emit("next");
    },
    goBack() {
      this.$emit("back");
    }
  }
};
</script>

<style scoped>
/* מעטפת כללית של העמוד - ללא פיקסלים */
.page-layout {
  position: relative;
  width: 100vw;
  height: 100vh;
  background-color: #7bc0f2;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  overflow: hidden;
  direction: rtl;
  box-sizing: border-box;
  padding: 0.5vh 0.5vw;
}

/* אזור עליון - סידור Flex לשלושה אזורים בשורה אחת */
.layout-header {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 10;
}

.header-right {
  display: flex;
  justify-content: flex-start;
  flex: 1;
}

.header-center {
  display: flex;
  justify-content: center;
  align-items: center;
  flex: 2;
}

.header-left {
  display: flex;
  justify-content: flex-end;
  flex: 1;
}

/* כפתור חזור */
.back-btn {
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
}

.back-btn-img {
  height: 9vh;
  max-height: 5.5rem;
  transition: transform 0.2s ease;
}

.back-btn-img:hover {
  transform: scale(1.1);
}

.back-btn-text {
  font-family: "Karantina-Light", sans-serif;
  font-size: 1.8rem;
  color: #ffffff;
  margin-top: 0.2rem;
}

/* סמלים */
.symbols {
  display: flex;
  align-items: center;
  gap: 1vw;
}

.symbol-img {
  height: 9vh;
  max-height: 5.5rem;
  object-fit: contain;
}

/* אזור התוכן המרכזי של העמוד */
.layout-content {
  flex-grow: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 80vh;
  z-index: 1;
}

/* אזור תחתון - כפתור הבא */
.layout-footer {
  width: 100%;
  display: flex;
  justify-content: flex-end;
  z-index: 10;
}

.next-btn {
  width: 25vw;
  max-width: 13rem;
  height: 7vh;
  max-height: 4.5rem;
  background-color: #992211;
  border-radius: 5rem;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transition: transform 0.2s ease, background-color 0.2s ease;
  box-shadow: 0 0.5vh 1.5vh rgba(0, 0, 0, 0.15);
}

.next-btn-text {
  font-family: "Karantina-Light";
  font-size: 2.2rem;
  color: #ffffff;
}

.next-btn:hover {
  transform: scale(1.08);
  background-color: #b52b18;
}

/* --- העיצוב החדש למצב חסום ואפור --- */
.next-btn.disabled {
  background-color: #7a7a7a !important; /* צבע אפור */
  cursor: not-allowed !important;
  pointer-events: none; /* מונע לחיצות ואירועי Hover */
  transform: none !important; /* מונע את ה-scale של ה-hover */
  box-shadow: none;
}

.next-btn.disabled .next-btn-text {
  color: #b0b0b0; /* טקסט אפור בהיר יותר */
}
</style>