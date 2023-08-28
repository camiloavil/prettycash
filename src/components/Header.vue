<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})
const getImageUrl = (path) => {
  return new URL(`/src/assets/${path}`, import.meta.url).href;
};
const reloadPage = () => {
  window.location.reload();
}
</script>

<template>
  <header>
    <img @click="reloadPage" :src="getImageUrl(`logo.svg`)" alt="Logo" />
    <h3><span>Pretty </span>Cash</h3>
  </header>
</template>

<style scoped>
header {
  width: 100%;
  margin: 3px auto;
  display: flex;
  align-items: center;
  justify-content: center;
}
h3 {
  margin: 0;
  padding: 0 12px;
}
img {
  height: 30px;
  /* cursor: pointer; */
}
.read-the-docs {
  color: #888;
}
</style>
