<script setup>
import { watch, ref, onMounted } from 'vue';
import theme from '../assets/scripts/theme.js';
const dark_theme = ref(window.matchMedia('(prefers-color-scheme: dark)').matches)
watch(dark_theme, async (newTheme) => {
    if (!newTheme) {
        theme.setLightTheme()
    } else {
        theme.setDarkTheme()
    }
});
</script>
<template>
    <div>
        <svg v-show="dark_theme" @click="dark_theme = !dark_theme" xmlns="http://www.w3.org/2000/svg" width="1.2em" height="1.2em" viewBox="0 0 32 32" class="block h-full">
            <path d="M16 12.005a4 4 0 1 1-4 4 4.005 4.005 0 0 1 4-4m0-2a6 6 0 1 0 6 6 6 6 0 0 0-6-6zM5.394 6.813l1.414-1.415 3.506 3.506L8.9 10.318zM2 15.005h5v2H2zm3.394 10.192L8.9 21.691l1.414 1.415-3.506 3.505zM15 25.005h2v5h-2zm6.687-1.899 1.414-1.415 3.506 3.506-1.414 1.414zM25 15.005h5v2h-5zm-3.313-6.101 3.506-3.506 1.414 1.415-3.506 3.505zM15 2.005h2v5h-2z" fill="currentColor"/>
        </svg>
        <svg v-show="!dark_theme" @click="dark_theme = !dark_theme" xmlns="http://www.w3.org/2000/svg" width="1.2em" height="1.2em" viewBox="0 0 32 32" class="block h-full">
            <path d="M13.502 5.414a15.075 15.075 0 0 0 11.594 18.194 11.113 11.113 0 0 1-7.975 3.39c-.138 0-.278.005-.418 0a11.094 11.094 0 0 1-3.2-21.584M14.98 3a1.002 1.002 0 0 0-.175.016 13.096 13.096 0 0 0 1.825 25.981c.164.006.328 0 .49 0a13.072 13.072 0 0 0 10.703-5.555 1.01 1.01 0 0 0-.783-1.565A13.08 13.08 0 0 1 15.89 4.38 1.015 1.015 0 0 0 14.98 3z" fill="currentColor"/>
        </svg>
    </div>
</template>
<style scoped>
div {
    display: flex;
    align-items: center;
    justify-content: center;
}
svg{
    height: 25px;
    width: 25px;
    border-radius: 20px;
    /* cursor: pointer; */
}
</style>