<template>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <label>Create Todo</label>
    <br><br>
    <input name="newTodo">
    <br><br>
    <button>Submit Todo</button>
  </form>
</template>

<script>
export default {
  setup() {
    function addNewTodo() {
      console.log('form submitted!!')
    }
    return {
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