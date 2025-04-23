<script setup>
import { ref, computed, watch } from 'vue'
import Watcher from './components/Watch.vue'
import Props from './components/Propss.vue'
import JSConfetti from 'js-confetti'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
])

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}

const confetti = new JSConfetti()

function showConfetti() {
  confetti.addConfetti()
}

const allCompleted = ref(false)

watch(todos, (newTodos) => {
  allCompleted.value = newTodos.every((todo) => todo.done)
  if (allCompleted.value) {
    showConfetti()
  }
}, { deep: true })
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" required placeholder="new todo">
    <button>Add Todo</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
    <button @click="hideCompleted = !hideCompleted">
      {{ hideCompleted ? 'Show all' : 'Hide completed' }}
    </button>
  </ul>

  <Watcher />
  <div>
    <Props /> 
  </div>
  
  <div>
    <h1 v-if="allCompleted">🎉 Congratulations!</h1>
  </div>
</template>

<style>
.done {
  text-decoration: line-through;
}
h1 {
  text-align: center;
  cursor: pointer;
  margin-top: 3em;
}
</style>