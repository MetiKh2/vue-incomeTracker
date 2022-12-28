<script setup>
import { ref } from 'vue';
const emit = defineEmits(['formHandler'])
let formData=ref({
    description:'',
    income:0,
    date:null
})
</script>

<template>
    <form @submit.prevent="emit('formHandler',formData)">
      <input type="text" placeholder="Income Description..." v-model="formData.description" />
      <input type="number" placeholder="Income Value..." v-model="formData.income" />
      <input type="date" placeholder="Income Date..." v-model="formData.date" />
      <input type="submit" value="SUBMIT" />
    </form>
  </template>

<style scoped>
  form {
    display: flex;
    justify-content: center;
    margin-top: 30px;
  }
  form input {
    color: #888;
    border: none;
    outline: none;
    font-size: 20px;
  }
  form input::placeholder {
    color: #AAA;
  }
  form input:not([type="submit"]) {
    display: block;
    background: #FFF;
    border: none;
    outline: none;
    padding: 5px 15px;
  }
  form input[type="submit"] {
    display: block;
    background: none;
    border: none;
    outline: none;
    color: #FFF;
    font-weight: 500;
    text-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
    padding: 5px 15px;
    background-color: #FFCE00;
    cursor: pointer;
  }
  form input:first-of-type {
    border-radius: 8px 0px 0px 8px;
  }
  form input:last-of-type {
    border-radius: 0px 8px 8px 0px;
  }
</style>