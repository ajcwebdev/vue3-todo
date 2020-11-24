# vue3-todo

## Setup

```
vue3-todo create todo
cd vue3-todo
yarn serve
```

```html
<template>
  <h1>Vue 3 Todo App</h1>
</template>

<script>
export default {

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
```

## Create New Todo Form

```html
<template>
  <h1>Vue 3 Todo App</h1>
  <form>
    <label>Create Todo</label>
    <br><br>
    <input>
    <br><br>
    <button>Submit Todo</button>
  </form>
</template>
```

## Call a function when the form is submitted

## Create a string property to store the user input
### Watch the property change as we type in the input

## Log the user input when the form is submitted

## Create an array property for todos

## Push the new todo into the todos array, with done: false

## Show the todos in a list

## Check done on a todo to mark it as done
### Show a line through the todo text

## Add a button to delete a todo

## Add a button to mark all todos as done