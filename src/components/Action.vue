<script setup>
import Modal from "./Modal.vue";
import { ref, defineEmits } from "vue";
const showModal = ref(false);
const title = ref("");
const amount = ref(0);
const description = ref("");
const movementType = ref("Ingreso");

const emit = defineEmits(["create"]);
const submit = () => {
  showModal.value = !showModal.value;
  emit("create", {
    title: title.value,
    description: description.value,
    amount: movementType.value === "Ingreso" ? amount.value : -amount.value,
    time: new Date(),
    id: new Date().getTime(),
  })
  title.value = "";
  description.value = "";
  amount.value = 0;
  movementType.value = "Ingreso";
}
</script>

<template>  
    <button @click="showModal=true" >Add movement</button>
    <Teleport to="#app">
        <Modal v-show="showModal" @close="showModal=false"> 
            <form @submit.prevent="submit">
                <div class="field">
                    <label>Title</label>
                    <input type="text" v-model="title" />
                </div>
                <div class="field">
                    <label>Amount</label>
                    <input type="number" v-model="amount" />
                </div>
                <div class="field">
                    <label>Description</label>
                    <textarea rows="4" v-model="description"></textarea>
                </div>
                <div class="field">
                    <label class="radio-label">
                        <input type="radio" v-model="movementType" value="Ingreso" />
                        <span>Income</span>
                    </label>
                    <label class="radio-label">
                        <input type="radio" v-model="movementType" value="Gasto" />
                        <span>Expense</span>
                    </label>
                </div>
                <div class="action">
                    <button>Add movement</button>
                </div>
            </form>
        </Modal>
    </Teleport>
</template>

<style scoped>
button {
  color: var(--color-text);
  font-size: 1.5rem;
  background-color: var(--color-background-mute);
  box-shadow: 0 1px 16px 0px var(--color-shadow);
  border: none;
  width: 100%;
  padding: 10px 30px;
  border-radius: 20px;
}

form {
  font-size: 1.24rem;
  width: 100%;
}

form .action {
  padding: 0 24px;
}

.field {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px 24px;
}

label {
  margin-bottom: 8px;
}
input,
textarea {
  font-size: 1.1rem;
  border: 2px solid var(--color-border);
  border-radius: 8px;
  padding: 8px;
}
input[type="number"] {
  text-align: right;
}
.radio-label {
  display: flex;
  align-items: center;
  margin-top: 8px;
}

.radio-label span {
  margin-top: 4px;
  margin-left: 8px;
}

input[type="radio"] {
  appearance: none;
  width: 1.24rem;
  height: 1.24rem;
  color: rgb(112, 112, 192);
  border: 2px solid rgb(112, 112, 192);
  border-radius: 50%;
}

input[type="radio"]:checked {
  background-color: rgb(112, 112, 192);
}
</style>