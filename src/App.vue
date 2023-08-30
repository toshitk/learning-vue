<template>
  <button @click="increment">count is: {{ count }}</button>
  <input v-model="text" placeholder="Type here">
  <button @click="toggle">toggle</button>
  <h1 v-if="awesome">Vue is {{ text }}</h1>
  <h1 v-else>Oh no 😢</h1>

  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>    
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>

  <p>Todo id: {{ todoId }}</p>
  <button @click="todoId++">Fetch next todo</button>
  <p v-if="!todoData">Loading...</p>
  <pre v-else>{{ todoData }}</pre>
</template>

<script setup>
import { ref, watch } from 'vue';

const count = ref(0)
const text = ref('')
const awesome = ref(true)
let id = 0
const newTodo = ref('')
const todos = ref([
  { id: id++, text: 'Learn HTML' },
  { id: id++, text: 'Learn JavaScript' },
  { id: id++, text: 'Learn Vue' }
])
const todoId = ref(1)
const todoData= ref(null)

function increment() {
  count.value++
}

function toggle() {
  awesome.value = !awesome.value
}

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}

async function fetchData() {
  todoData.value = null
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  )
  todoData.value = await res.json()
}
fetchData()
watch(todoId, fetchData)
</script>
