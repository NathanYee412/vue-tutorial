<script setup>
import { reactive, ref } from 'vue';
import Test from './Test.vue';
import TodoList from './TodoList.vue';
const state = reactive({ count: 0 });
const test = ref('hello world');
function increment() {
  state.count++;
}
</script>

<template>
  <TodoList />
  <Test />
  <h1>{{ test }}</h1>
  <button @click="increment">
    {{ state.count }}
  </button>
</template>

<style>
button {
    color: red;
}
</style>