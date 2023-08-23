<script setup>
import 'animate.css';
// import { ref } from 'vue'

defineProps({
  msg: String,
})
const getImageUrl = (path) => {
  return new URL(`/src/assets/${path}`, import.meta.url).href;
};
</script>

<template>
  <img :src="getImageUrl(`logo.svg`)" alt="logo" /> 
</template>

<style scoped>
img{
  margin: 0 auto;

  width: 250px;
  animation: flip; /* referring directly to the animation's @keyframe declaration */
  animation-duration: 800ms; /* don't forget to set a duration! */
}

</style>
