# vue3-todo

This project is based on the excellent video [Intro to Vue 3 + Composition API: Build a Todo App](https://www.youtube.com/watch?v=rncY1tlWShM) by [Coding Garden with CJ](https://www.youtube.com/channel/UCLNgu_OupwoeESgtab33CCw).

## Setup

```
vue create vue3-todo
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
  <form @submit="addNewTodo">
    <label>Create Todo</label>
    <br><br>
    <input name="newTodo">
    <br><br>
    <button>Submit Todo</button>
  </form>
</template>
```

![01-create-new-todo-form](./assets/01-create-new-todo-form.jpg)

## Call a function when the form is submitted

```html
<form @submit.prevent="addNewTodo">
```

```javascript
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
```

![02-call-a-function-when-the-form-is-submitted](./assets/02-call-a-function-when-the-form-is-submitted.jpg)

## Create a string property to store the user input

```javascript
import { ref } from 'vue'

export default {
  setup() {
    const newTodo = ref('');

    return {
      newTodo,
    }
  }
}
```

```html
<input v-model="newTodo" name="newTodo">
```

### Watch the property change as we type in the input

```html
<h2>{{newTodo}}</h2>
```

![03-watch-the-property-change-as-we-type-in-the-input](./assets/03-watch-the-property-change-as-we-type-in-the-input.jpg)

## Log the user input when the form is submitted

```javascript
function addNewTodo() {
  console.log(newTodo.value)
}
```

![04-log-the-user-input-when-the-form-is-submitted.jpg](./assets/04-log-the-user-input-when-the-form-is-submitted.jpg)

## Create an array property for todos

```javascript
export default {
  setup() {
    const todos = ref([])

    return {
      todos,
    }
  }
}
```

## Push the new todo into the todos array, with done: false

## Show the todos in a list

## Check done on a todo to mark it as done
### Show a line through the todo text

## Add a button to delete a todo

## Add a button to mark all todos as done