<template>
    <page-layout @next="$emit('next')" @back="$emit('back')">
      
  
     
      
  
    </page-layout>
  </template>
  
  <script>
  import PageLayout from './PageLayout.vue';
  
  export default {
    name: "Importance",
    components: { PageLayout },
    emits: ["next", "back"]
  }
  </script>
  
  <style scoped>
  
  
</style>