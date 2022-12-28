<script setup>
import Header from './components/Header.vue'
import Form from './components/Form.vue'
import IncomeItem from './components/IncomeItem.vue'
import { computed, onMounted, ref } from 'vue';

let incomes = ref([])
const totalIncome = computed(() => {
  const res = incomes.value.map(i => i.income)
  return res.reduce((partialSum, a) => partialSum + a, 0);
})
function formHandler(data) {
  if (data.description && data.income) {
    incomes.value.push({
      ...data,
      id: new Date().getTime()
    })
    console.log(incomes.value);
    setLocalStorage()
  }
}
function setLocalStorage() {
  localStorage.setItem('incomes', JSON.stringify(incomes.value));
}
onMounted(() => {
  incomes.value = JSON.parse(localStorage.getItem('incomes')) || []
  console.log(incomes.value);
})
function removeIncome(id) {
  console.log(id);
  incomes.value = incomes.value.filter(i => i.id != id)
  setLocalStorage()
}
</script>

<template>
  <Header :totalIncome="totalIncome"></Header>
  <Form @formHandler="formHandler"></Form>
  <div class="income-list">
    <IncomeItem v-for="income in incomes" :key="income.id" :income="income" @removeIncome="removeIncome" />
  </div>
</template>
<style>
.income-list {
  margin-top: 30px;
  padding: 15px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}

body {
  background: #EEE;
}
</style>