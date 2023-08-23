<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})
const getImageUrl = (path) => {
  return new URL(`/src/assets/${path}`, import.meta.url).href;
};
</script>

<template>
  <header>
        <img @click="location.reload();" :src="getImageUrl(`logo.svg`)" alt="Logo" />
        <h3><span>Pretty </span>Cash</h3>
        <span></span>
    </header>
</template>

<style scoped>
header {
  display: flex;
}
h3 {
  margin: 0;
}
img {
  height: 25px;
  /* cursor: pointer; */
}
.read-the-docs {
  color: #888;
}
</style>
