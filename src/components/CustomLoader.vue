<script setup>
import 'animate.css';
// import { ref } from 'vue'

defineProps({
  qty: {
    type: Number,
    defautl: 5
  },
})
const getImageUrl = (path) => {
  return new URL(`/src/assets/${path}`, import.meta.url).href;
};
</script>

<template>
  <div>
    <img :src="getImageUrl(`logo.svg`)" alt="logo" /> 
    <section class="dots-container">
      <div class="dot"></div>
      <div class="dot"></div>
      <div class="dot"></div>
      <div class="dot"></div>
      <div class="dot"></div>
    </section>
  </div>
</template>

<style scoped>
div {
  height: 100vh;
  display: grid;
  place-content: center;
}
/* body {
  background-color: black;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
} */
img{
  margin: 15px auto;
  width: 250px;
  animation: flip; /* referring directly to the animation's @keyframe declaration */
  animation-duration: 1200ms; /* don't forget to set a duration! */
}
.dots-container {
  margin-top: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  width: 100%;
}
.dot {
  height: 20px;
  width: 20px;
  margin-right: 10px;
  border-radius: 10px;
  background-color: #b3d4fc;
  animation: pulse 1.5s
  infinite ease-in-out;
}
.dot:last-child {
  margin-right: 0;
}
.dot:nth-child(1) {
  animation-delay: -0.3s;
}
.dot:nth-child(2) {
  animation-delay: -0.1s;
}
.dot:nth-child(3) {
  animation-delay: 0.1s;
}

@keyframes pulse {
  0% {
    transform: scale(0.8);
    background-color: #0e3bc0;
    box-shadow: 0 0 0 0 rgba(178, 212, 252, 0.7);
  }
  50% {
    transform: scale(.9);
    background-color: #00fffc;
    box-shadow: 0 0 0 5px rgba(178, 212, 252, 0.325);
  }
  100% {
    transform: scale(0.8);
    background-color: #0e3bc0;
    box-shadow: 0 0 0 0 rgb(18, 55, 97);
  }
}

</style>
