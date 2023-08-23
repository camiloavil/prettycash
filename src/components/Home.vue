<script setup>
import Layout from './Layout.vue';
import Header from './Header.vue';
import Resume from './Resume/Index.vue';
import Movements from './Movements.vue';
import { ref } from 'vue';

const label = ref(null);
const amount = ref(null);

</script>

<template>
  <Layout>
      <template #header>
          <Header></Header>
      </template>
      <template #resume>
        <Resume :totalLabel="'Ahorro Total'" :label="label" :totalAmount="100000" :amount="amount">
          <template #graphic>
              graphic
          </template>
          <template #action>
              action
          </template>
        </Resume>
      </template>
      <template #movements>
        <Movements/>
      </template>
  </Layout>
</template>

<style scoped>
</style>
