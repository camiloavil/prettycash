<script setup>
    import { ref } from "vue";
    const showMovements = ref(false);
</script>

<template> 
    <div class="header">
        <slot name="header"></slot>
    </div> 
    <div class="resume">
        <slot name="resume"></slot>    
    </div>
    <div class="movements">
        <div class="head" @click="showMovements = !showMovements">
            <div class="grip"></div>
        </div>
        <div class="body" v-show="showMovements">
            <slot name="movements"></slot>
        </div>
    </div>
</template>

<style scoped>

.header{
  display: flex;
}

.movements {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 8px 0;
  box-sizing: border-box;

  z-index: 1;
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  flex-direction: column;
  bottom: 0;
  width: 100%; 
  max-width: 480px;

  background-color: var(--color-background-mute);
  box-shadow: 0 -4px 19px 0 var(--color-shadow);
  border-top-left-radius: 25px;
  border-top-right-radius: 25px;
}

.movements .head {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 12px;
  width: 100%;
  box-sizing: border-box;
}

.movements .body {
  height: 75vh;
  width: 100%;
}

.movements .grip {
  width: 120px;
  height: 8px;
  background-color: var(--color-shadow);
  border-radius: 4px;
}
</style>