<template>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <label>Create Todo</label>
    <br><br>
    <input v-model="newTodo" name="newTodo">
    <br><br>
    <button>Submit Todo</button>
  </form>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const newTodo = ref('')
    const todos = ref([])

    function addNewTodo() {
      todos.value.push({
        done: false,
        content: newTodo.value,
      })
    }
    
    return {
      todos,
      newTodo,
      addNewTodo,
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