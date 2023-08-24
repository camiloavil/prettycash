<script setup>
import { toRefs, computed } from 'vue';

const emit = defineEmits(["remove"]);

const props = defineProps({
    id: {
        type: Number,    
    },
    title: {
        type: String,
    },
    description:{
        type: String,
    },
    amount:{
        type: Number,
    }
});

const { id, title, description, amount } = toRefs(props);

const getImageUrl = (path) => {
  return new URL(`/src/assets/${path}`, import.meta.url).href;
};

const currencyFormatter = new Intl.NumberFormat("es-CO", {
  style: "currency",
  currency: "COP",
});

const amountCurrency = computed(
    () => currencyFormatter.format(amount.value)
);

const isNegative = computed(
    () => amount.value < 0);

const remove = () => {
//   console.log(`borrar ${id.value}`);
  emit("remove", id.value);
}

</script>

<template>
    <div class="movement">
        <div class="content">
            <h4>{{title}}</h4>
            <p>{{description}}</p>
        </div>
        <div class="action">
            <img @click="remove" :src="getImageUrl(`trash-icon.svg`)" alt="borrar">
            <p :class="{'red': isNegative,'green': !isNegative}">{{amountCurrency}}</p>
        </div>
    </div>
</template>

<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e97a12;
  border-radius: 8px;
  box-sizing: border-box;
}

.movement .content {
  width: 100%;
}

.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}

h4,
p {
  margin: 0;
  padding: 0;
}

h4 {
  margin-bottom: 8px;
}

.movement .action img {
  margin-bottom: 16px;
}

.red {
    color: red;
}

.green {
    color: green;
}
</style>