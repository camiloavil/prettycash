<script setup>
import { ref, computed, toRefs, defineEmits, watch } from 'vue';
const emit = defineEmits(['select']);
const props = defineProps({
    amounts : {
        type: Array,
        default: () => [],
    }
});
const { amounts } = toRefs(props);
const xLength = ref(300);
const yLength = ref(250);

const showPointer = ref(false);
const pointer = ref(0);
const tap = ({ target, touches }) => {
    showPointer.value = true;
    const elementWidth = target.getBoundingClientRect().width;
    const elementX = target.getBoundingClientRect().x;
    const touchX = touches[0].clientX;
    pointer.value = ((touchX - elementX) * xLength.value) / elementWidth;
}
const untap = () => {
    showPointer.value = false;
}
const amountToPixels = (amount) => {
    //Ajustar eje Y
    const min = Math.min(...amounts.value);
    const max = Math.max(...amounts.value);
    
    const minmax = Math.abs(max) + Math.abs(min);
    const amountAbs = amount + Math.abs(min);
    
    return yLength.value - ((amountAbs * yLength.value) / minmax);
    // return yLength.value - ((amountAbs * 100) / minmax) * (yLength.value / 100);
}
const zero = computed(() => {
    return amountToPixels(0);
})
const points = computed(() => {
    const total = amounts.value.length;
    return amounts.value.reduce((points, amount, i) => {
        const x = (xLength.value/total) * (i + 1);
        const y = amountToPixels(amount);
        return `${points} ${x},${y}`;
    },`0,${zero.value}`);
})

watch(pointer, (value) => {
    const index = Math.ceil((value / (xLength.value / amounts.value.length)));
    if (index < 0 || index > amounts.value.length) return;
    emit("select", amounts.value[index - 1]);
});
</script>

<template>
    <div>
        <svg @touchstart="tap" @touchmove="tap" @touchend="untap" :viewBox="`0 0  ${xLength} ${yLength}`" >
            <line stroke="gray" stroke-width="2" x1="0" :y1="zero" x2="300" :y2="zero"/>
            <polyline fill="none" stroke="#0689B0" stroke-width="2" :points="points"/>
            <line v-show="showPointer" stroke="#04b500" stroke-width="2" :x1="pointer" y1="0" :x2="pointer" :y2="yLength"/>
        </svg>
        <p>Ultimos 30 dias</p>
    </div>
</template>
<style scoped>
svg {
  width: 100%;
}
p {
  text-align: center;
}
</style>