<template>
  <page-layout @next="$emit('next')" @back="$emit('back')">
    <template #main-content>
    <div class="page">
        <h3><strong>תרגול מסכם</strong> </h3>
        <p>למדנו על כל הטפסים בלומדה, הבנו את משמעותם וחשיבותם להליך משפטי תקין</p>
        <p>כעת נעבור לתרגול שיכלול מספר שאלות ותבחנו את הבנתכם</p>
        <p>אם אתם מרגישים שתרצו לעבור על החומר פעם נוספת זה הזמן - לא תהיה אפשרות נוספת</p>
        <p>בהצלחה!!!</p>
    </div>
</template>
  </page-layout>
</template>

<script>
 import PageLayout from './PageLayout.vue';

export default {
    name: "practice",
    components: { PageLayout },
    emits: ["next", "back"]
  
}
</script>

<style>
.page {
   height: 75vh;
    width: 70vw;
    text-align: center;
    top: -2vh;
}

.page h3{
    font-family: "Karantina-Bold";
    font-size: 7rem;
    margin-bottom: 1.5rem;
    letter-spacing: 0.5rem;
}

.page p{
    font-family: "ElonWiess";
    font-size: 2.8rem;
    margin-bottom: 1.5rem;
    
}
</style>