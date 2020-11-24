<template>
  <h1>Vue 3 Todo App</h1>

  <form @submit.prevent="addNewTodo">
    <label>Create Todo</label>
    <br><br>
    <input v-model="newTodo" name="newTodo">
    <br><br>
    <button>Submit Todo</button>
    <br><br>
  </form>

  <button @click="removeAllTodos">
    Remove All
  </button>
  <br><br>
  <button @click="markAllDone">
    Mark All Done
  </button>

  <ul>
    <li
      v-for="todo in todos"
      v-bind:key="todo.id"
      class="todo"
    >
      <h3
        :class="{ done: todo.done }"
        @click="toggleDone(todo)"
      >
        {{todo.content}}
      </h3>
      <button @click="removeTodo(todo)">
        Remove Todo
      </button>
    </li>
  </ul>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const newTodo = ref('')
    const todos = ref([])

    const addNewTodo = () => {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      })
      newTodo.value = ''
    }

    const toggleDone = (todo) => {
      todo.done = !todo.done
    }

    const removeTodo = (index) => {
      todos.value.splice(index, 1)
    }

    const markAllDone = () => {
      todos.value.forEach(
        (todo) => todo.done = true
      )
    }

    const removeAllTodos = () => {
      todos.value = []
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAllTodos,
    }
  }
}
</script>

<style>
.todo {
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
</style>