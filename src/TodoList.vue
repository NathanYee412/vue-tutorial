<script setup>
  import { ref, computed, onMounted } from 'vue'

let id = 0

  const newTodo = ref('')
  const hideCompleted= ref(false)
  const title = ref(null)
  const todos = ref([
    {id: id++, text: "sample", done: true},
    {id: id++, text: "sample2", done: true},
    {id: id++, text: "sample3", done: false}
  ])

  // its a computed ref that computes its value based on other reactive data sources
  // uses todos ref object
  const filteredTodos = computed(() => {
    return hideCompleted.value
      ? todos.value.filter((t) => !t.done)
      : todos.value
  })

  // Manually change DOM elements using onMounted 
  // h1 tag title is changed from hello to Todo list
  onMounted(() => {
    title.value.textContent = "Todo List"
  })

  function addTodo() {
    todos.value.push({id: id++, text: newTodo.value, done: false})
    newTodo.value = ''
  }

  function removeTodo(todo) {
    todos.value = todos.value.filter((t) => t !== todo)
  }
</script>



<template>
  <h1 ref="title">Hello</h1>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{done: todo.done}">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide Completed'}}
  </button>
</template>

<style>
  .done {
    text-decoration: line-through;
  }

</style>