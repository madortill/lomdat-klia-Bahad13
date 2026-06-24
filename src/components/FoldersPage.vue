<template>
  <page-layout @next="$emit('next')" @back="$emit('back')">
    <template #main-content>
        <div class="four">
        <img src="@/assets/media/Group 10.svg" class="f-img">
        <img src="@/assets/media/Group 11.svg" class="f-img">
        <img src="@/assets/media/Group 12.svg" class="f-img">
        <img src="@/assets/media/Group 13.svg" class="f-img">
    </div>
    </template>
  </page-layout>
</template>

<script>
import PageLayout from './PageLayout.vue'
export default {
    name:"FoldersPage",
  components: { PageLayout },
  emits: ["next", "back"]
}
</script>

<style>
.four {
    width:80vw;
    height: 80vh;
}

.f-img{
    object-fit: cover;
}

</style>