<script setup>
import Layout from './Layout.vue';
import Header from './Header.vue';
import Resume from './Resume/Index.vue';
import Graphic from './Resume/Graphic.vue';
import Movements from './Movement/Index.vue';
import Action from './Action.vue';
import { ref } from 'vue';

const label = ref(null);
const amount = ref(null);
const movements = ref([{
                id: 0,
                title: "Movimiento 1",
                description: "Lorem ipsum dolor sit amet",
                amount: 1000,
            }, {
                id: 1,
                title: "Movimiento 2",
                description: "Lorem ipsum dolor sit amet",
                amount: 1000,
            }, {
                id: 2,
                title: "Movimiento 3",
                description: "Lorem ipsum dolor sit amet",
                amount: -1000,
            }, {
                id: 3,
                title: "Movimiento 4",
                description: "Lorem ipsum dolor sit amet",
                amount: -1000,
            }, {
                id: 4,
                title: "Movimiento 5",
                description: "Lorem ipsum dolor sit amet",
                amount: 1000,
            }, {
                id: 6,
                title: "Movimiento 7",
                description: "Lorem ipsum dolor sit amet",
                amount: 1000,
            }, {
                id: 7,
                title: "Movimiento 8",
                description: "Lorem ipsum dolor sit amet",
                amount: -1000,
            }, {
                id: 8,
                title: "Movimiento 9",
                description: "Lorem ipsum dolor sit amet",
                amount: 1000,
            }]);

const amounts = ref([100, 200, 500, 200, -400, -100, -600, 0, 300, 800]);
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
