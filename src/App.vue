<template>
  <button @click="increment">count is: {{ count }}</button>
  <input v-model="text" placeholder="Type here">
  <button @click="toggle">toggle</button>
  <h1 v-if="awesome">Vue is {{ text }}</h1>
  <h1 v-else>Oh no 😢</h1>
</template>

<script setup>
import { ref } from 'vue';

const count = ref(0)
const text = ref('')
const awesome = ref(true)

function increment() {
  count.value++
}

function toggle() {
  awesome.value = !awesome.value
}
</script>
