<template>
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
    name:"FoldersPage",
  components: { PageLayout },
  emits: ["next", "back"]
}
</script>

<style>
.four {
    width:80vw;
    height: 81vh;
}

.f-img{
    object-fit: cover;
}

</style>