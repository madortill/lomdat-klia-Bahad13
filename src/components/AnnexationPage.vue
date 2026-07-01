<!-- <template>
  <page-layout>
     <template #main-content>
        <img src="@/assets/media/files/deposit.jpeg" alt="tofes" class="sipoach-tofes"/>
        <p> צו סיפוח זה מורה על התייצבות למעצר מהיחידה למטרת כליארה ולמטרת חזרה ליחידה לאחר שחרור</p>
     </template>
  </page-layout>
</template>

<script>
import PageLayout from './PageLayout.vue'
export default {
    name: "AnnextionPage",
  components: { PageLayout },

}
</script>

<style>
.sipoach-tofes {
    width: 50vw;

}

</style> -->

<template>
    <page-layout>
       <template #main-content>
         <div class="content-container">
           <!-- עטיפה לתמונה כדי שהסיבוב לא ישבור את ה-Flexbox -->
           <div class="image-wrapper">
             <img src="@/assets/media/files/deposit.jpeg" alt="tofes" class="sipoach-tofes"/>
           </div>
           <p class="sipoach-text">
             צו סיפוח זה מורה על התייצבות למעצר מהיחידה למטרת כליארה ולמטרת חזרה ליחידה לאחר שחרור
           </p>
         </div>
       </template>
    </page-layout>
  </template>
  
  <script>
  import PageLayout from './PageLayout.vue'
  
  export default {
    name: "AnnextionPage",
    components: { PageLayout },
  }
  </script>
  
  <style scoped>
  .content-container {
    display: flex;
    flex-direction: row-reverse; 
    align-items: center;        
    justify-content: center;    
    gap: 5vw;                   
    width: 100%;
  }
  
  /* אלמנט העטיפה ששומר על המקום הפיזי של התמונה במסך */
  .image-wrapper {
    width: 50vw;                /* הרוחב שיוקצה לתמונה המסובבת */
    height: 30vw;               /* הגובה המקסימלי שהיא תתפוס כשהיא שוכבת */
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: visible;
  }
  
  /* עיצוב התמונה והסיבוב שלה */
  .sipoach-tofes {
    /* כאן קורה הסיבוב! אם היא מסתובבת לכיוון הלא נכון, שני ל- -90deg */
    transform: rotate(90deg);   
    
    /* בגלל שהתמונה המקורית הייתה לאורך (גבוהה), כשאנחנו מסובבים אותה לרוחב, 
       הגובה המקורי שלה הופך להיות הרוחב החדש שלה. לכן נגדיר את ה-max-width */
    max-width: 35vw;            
    height: auto;               
    object-fit: contain;
  }
  
  .sipoach-text {
    background-color:  rgba(239, 241, 246, 0.95); 
    color: #000; 
    width: 20vw;  
    font-family: "Karantina-light";              
    font-size: 2.5rem;            
    line-height: 1.4;           
    text-align: right;          
    margin: 0;
    padding: 1rem;
    border-radius: 2rem;
    text-align: center;
   
  }
  </style>