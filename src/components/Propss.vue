<script setup>
import { ref } from 'vue'
import ChildComp from './ChildProps.vue'
  
const newTodo = ref('')
const todo= ref('')
const greeting = ref('Hello from parent')
function Props() {
  todo.value= newTodo.value
  newTodo.value = ''
}
</script>

<template>
  <ul>
  <form @submit.prevent="Props">
    <input v-model="newTodo" required placeholder="Pass props">
    <button>Pass</button>
  </form>
  </ul>
  <ChildComp :msg= todo />
</template>