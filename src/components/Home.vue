<script setup>
import Layout from './Layout.vue';
import Header from './Header.vue';
import Resume from './Resume/Index.vue';
import Graphic from './Resume/Graphic.vue';
import Movements from './Movement/Index.vue';
import Action from './Action.vue';
import { ref, computed } from 'vue';

const limitDays = ref(30);
const label = ref(null);
const amount = ref(null);
const movements = ref([
        {
          id: 0,
          title: "Movimiento 1",
          description: "Lorem ipsum dolor sit amet",
          amount: 100,
          time: new Date("2023-08-01"),
        },
        {
          id: 1,
          title: "Movimiento 2",
          description: "Lorem ipsum dolor sit amet",
          amount: 200,
          time: new Date("2023-08-02"),
        },
        {
          id: 2,
          title: "Movimiento 3",
          description: "Lorem ipsum dolor sit amet",
          amount: 500,
          time: new Date("2023-08-02"),
        },
        {
          id: 3,
          title: "Movimiento 4",
          description: "Lorem ipsum dolor sit amet",
          amount: 200,
          time: new Date("2023-08-02"),
        },
        {
          id: 4,
          title: "Movimiento 5",
          description: "Lorem ipsum dolor sit amet",
          amount: -400,
          time: new Date("2023-08-07"),
        },
        {
          id: 5,
          title: "Movimiento 6",
          description: "Lorem ipsum dolor sit amet",
          amount: -600,
          time: new Date("2023-08-07"),
        },
        {
          id: 6,
          title: "Movimiento 7",
          description: "Lorem ipsum dolor sit amet",
          amount: -300,
          time: new Date("2023-08-09"),
        },
        {
          id: 7,
          title: "Movimiento 8",
          description: "Lorem ipsum dolor sit amet",
          amount: 100,
          time: new Date("2023-08-10"),
        },
        {
          id: 8,
          title: "Movimiento 9",
          description: "Lorem ipsum dolor sit amet",
          amount: 300,
          time: new Date("2023-08-15"),
        },
        {
          id: 9,
          title: "Movimiento 10",
          description: "Lorem ipsum dolor sit amet",
          amount: 500,
          time: new Date("2023-08-15"),
        },
        {
          id: 10,
          title: "Movimiento 10",
          description: "Lorem ipsum dolor sit amet",
          amount: 500,
          time: new Date("2023-06-15"),
        }]);

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
        const acumulator = lastMovements.slice(0, i);
        return acumulator.reduce((suma, movement) => {
            return suma + movement.amount
        }, 0);
    });
    // console.log(data);
    return data;
});
const remove = () => {
    console.log(`borrar ${id.value}`);
}
</script>

<template>
  <Layout>
      <template #header>
          <Header></Header>
      </template>
      <template #resume>
        <Resume :totalLabel="'Ahorro Total'" :label="label" :totalAmount="100000" :amount="amount">
          <template #graphic>
            <Graphic :amounts="amounts"/>
          </template>
          <template #action>
              <Action/>
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
