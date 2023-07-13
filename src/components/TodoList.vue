<script setup>
import { ref } from 'vue'
import TodoDetails from './TodoDetails.vue'

let id = 0

const todos = ref([
  { id: id++, name: 'Learn JavaScript', description: 'TodoDescription blabla', done: false },
  { id: id++, name: 'Learn Vue', description: 'TodoDescription blabla', done: false },
  { id: id++, name: 'Play around in JSFiddle', description: 'TodoDescription blabla', done: true },
  { id: id++, name: 'Build something awesome', description: 'TodoDescription blabla', done: false }
])



let newTodo = ref({
  name: '',
  description: ''
})
let selectedTodo = ref(null)

function add() {
  todos.value.push({
    id: id++,
    name: newTodo.value.name,
    description: newTodo.value.description,
    done: false
  })
  newTodo.value.name = ''
  newTodo.value.description = ''
  console.log(todos.value)
}

function selectTodo(todo) {
  selectedTodo.value = todo
}

function deleteTodo (id) {
  todos.value = todos.value.filter(todo => todo.id !== id)
}


console.log(todos.value)
</script>

<template>
  <div>
    <h1>Todo List</h1>
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <p>{{ todo.name }}</p>
        <input type="checkbox" v-model="todo.done" checked />
        <button @click="selectTodo(todo)">Show Details</button>
        <button @click="deleteTodo(todo.id)">Delete</button>

      </li>
    </ul>
  </div>

  <form action="" @submit.prevent="add(newTodo)">
    <input type="text" v-model="newTodo.name" />
    <br />
    <input type="text" v-model="newTodo.description" />
    <input type="submit" value="Ajouter">
  </form>

  <TodoDetails :selectedTodo="selectedTodo" />
</template>
