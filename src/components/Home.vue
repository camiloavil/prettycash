<script setup>
import Layout from './Layout.vue';
import MyHeader from './Header.vue';
import Resume from './Resume/Index.vue';
import Graphic from './Resume/Graphic.vue';
import Movements from './Movement/Index.vue';
import Action from './Action.vue';
import { ref, toRefs, computed, onMounted } from 'vue';

const limitDays = ref(30);
const label = ref(null);
const amount = ref(null);
const movements = ref([]);

onMounted(() => {
  const storage = JSON.parse(localStorage.getItem("movements"));
  if (storage === null) {
    movements.value = [];
    return;
  }
  movements.value = storage;
  if (Array.isArray(movements.value)) {
    movements.value = movements.value.map(m => {
      return { ...m, time: new Date(m.time) };
    });
  }
});

const amounts = computed(() => {
    const lastMovements = movements.value.filter(m => {
        const limitDay = new Date();
        limitDay.setDate(limitDay.getDate() - limitDays.value);
        return m.time > limitDay;
    }).map(m => {return {amount: m.amount, time: m.time};})
    // console.log(lastMovements);

    // const datesArray = lastMovements.map(movement => movement.time.toISOString().split('T')[0]);
    // const uniqueDatesArray = [...new Set(datesArray)];
    // console.log(uniqueDatesArray);

    // const TotalByDay = uniqueDatesArray.map(date => {
    //     const movementsOfDay = lastMovements.filter(m => {
    //         return m.time.toISOString().split('T')[0] === date
    //     })
    //     return movementsOfDay.reduce((total, movement) => {
    //         return total + movement.amount
    //     },0);
    // });

    // console.log(lastDays);
    const data = lastMovements.map((m, i) => {
        const acumulator = lastMovements.slice(0, (i + 1));
        return acumulator.reduce((suma, movement) => {
            return suma + movement.amount
        }, 0);
    });
    // console.log(data);
    return data;
});
const totalAmount = computed(() => {
  return movements.value.reduce((total, movement) => {
    return total + movement.amount
  },0);
})
const create = (movement) => {
    movements.value.push(movement);
    save();
};
const remove = (id) => {
    movements.value = movements.value.filter(m => m.id !== id);
    console.log(`borrar ${id}`);
    save();
};
const selectedDate = (amountSelected) => {
    // console.log(amountSelected);
    amount.value = amountSelected;
};
const save = () => {
  localStorage.setItem("movements", JSON.stringify(movements.value));
}
</script>

<template>
  <Layout>
      <template #header>
        <MyHeader/>
      </template>
      <template #resume>
        <Resume :totalLabel="'Total Savings'" :label="label" :totalAmount="totalAmount" :amount="amount">
          <template #graphic>
            <Graphic :amounts="amounts" @select="selectedDate" />
          </template>
          <template #action>
              <Action @create="create"/>
          </template>
        </Resume>
      </template>
      <template #movements>
        <Movements @remove="remove" :movements="movements"/>
      </template>
  </Layout>
</template>

<style scoped>

</style>
