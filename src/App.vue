<script setup>

import { ref } from 'vue';


let id = ref(0);
let newItem = ref('')

const shoppingList = ref([
  { id: id++, text: 'Hamburger'},
  { id: id++, text: 'Hotdog'},
  { id: id++, text: 'Buns'},
  { id: id++, text: 'Ketchup'},
]);


function addToList(todo) {
  shoppingList.value.push({id: id++, text: newItem.value });
  newItem.value = '';
}


</script>

<template>
  <div class="container">
    <h1>Shopping List</h1>
    <form @submit.prevent="addToList">
      <input v-model="newItem">
    </form>
    <ul>
      <li v-for="item in shoppingList" :key="shoppingList.id">
        <p>{{ item.text }}</p>
      </li>
    </ul>
  </div>
</template>

<style>
.container {
  margin: 0 auto;
  background-color: red;
}

</style>