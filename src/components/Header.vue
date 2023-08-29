<script setup>
import ToggleTheme from './ToggleTheme.vue';
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
    <toggle-theme />
  </header>
</template>

<style scoped>
header {
  display: flex;
  width: 100%;
  padding: 8px 30px;
  align-items: center;
  justify-content: space-between;
}
h3 {
  margin: 0;
}
img {
  height: 30px;
}
</style>
