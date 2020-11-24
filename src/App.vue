<template>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <label>Create Todo</label>
    <br><br>
    <input v-model="newTodo" name="newTodo">
    <br><br>
    <button>Submit Todo</button>
  </form>
  <ul>
    <li v-for="todo in todos" v-bind:key="todo.id">
      <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
        {{todo.content}}
      </h3>
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

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
    }
  }
}
</script>

<style>
.done {
  text-decoration: line-through;
}
</style>