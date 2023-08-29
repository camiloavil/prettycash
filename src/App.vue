<script setup>
// import Init from './components/Init.vue'
import Init from './components/CustomLoader.vue'
import theme from './assets/scripts/theme.js';
import { ref, defineAsyncComponent, onMounted } from 'vue'

const dark_theme = ref(window.matchMedia('(prefers-color-scheme: dark)').matches)
const Home = defineAsyncComponent(() => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(import("./components/Home.vue"));
    }, 1500);
  });
});
onMounted(() => {
    if (dark_theme.value) {
        theme.setDarkTheme()
    } else {
        theme.setLightTheme()
    }
});
</script>

<template>
  <Suspense>
    <template #default>  
      <Home/>
    </template>
    <template #fallback>
      <Init/>
    </template>
  </Suspense>
</template>

<style scoped>
/* .logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
} */
</style>
