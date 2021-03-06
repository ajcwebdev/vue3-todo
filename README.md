# vue3-todo

This project is based on the excellent video [Intro to Vue 3 + Composition API: Build a Todo App](https://www.youtube.com/watch?v=rncY1tlWShM) by [Coding Garden with CJ](https://www.youtube.com/channel/UCLNgu_OupwoeESgtab33CCw).

## Setup

```
vue create vue3-todo
cd vue3-todo
code .
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
```

## Create New Todo Form

```html
<template>
  <h1>Vue 3 Todo App</h1>
  <form>
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
    const addNewTodo = () => {
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
const addNewTodo = () => {
  console.log(newTodo.value)
}
```

![04-log-the-user-input-when-the-form-is-submitted](./assets/04-log-the-user-input-when-the-form-is-submitted.jpg)

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

## Push the new todo into the todos array

```javascript
const addNewTodo = () => {
  todos.value.push({
    id: Date.now(),
    done: false,
    content: newTodo.value,
  })
  newTodo.value = ''
}
```

## Show the todos in a list

```html
<ul>
  <li v-for="todo in todos" v-bind:key="todo.id">
    <h3>{{todo.content}}</h3>
  </li>
</ul>
```

![05-show-the-todos-in-a-list](./assets/05-show-the-todos-in-a-list.jpg)

## Check done on a todo to mark it as done

```html
<h3 @click="toggleDone(todo)">{{todo.content}}</h3>
```

```javascript
const toggleDone = (todo) => {
  todo.done = !todo.done
}

return {
  toggleDone,
}
```

### Show a line through the todo text

```html
<li class="todo">

<style>
  .todo {
    cursor: pointer;
  }
  .done {
    text-decoration: line-through;
  }
</style>
```

```html
<h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
  {{todo.content}}
</h3>
```

![06-show-a-line-through-the-todo-text](./assets/06-show-a-line-through-the-todo-text.jpg)

## Add a button to delete a todo

```html
<button @click="removeTodo(todo)">
  Remove Todo
</button>
```

```javascript
const removeTodo = (index) => {
  todos.value.splice(index, 1)
}

return {
  removeTodo,
}
```

![07-add-a-button-to-delete-a-todo](./assets/07-add-a-button-to-delete-a-todo.jpg)

## Add a button to mark all todos as done

```html
<button @click="markAllDone">
  Mark All Done
</button>
```

```javascript
const markAllDone = () => {
  todos.value.forEach(
    (todo) => todo.done = true
  )
}
return {
  markAllDone,
}
```

![08-add-a-button-to-mark-all-todos-as-done](./assets/08-add-a-button-to-mark-all-todos-as-done.jpg)

## Add a button to remove all todos

```html
<button @click="removeAllTodos">
  Remove All
</button>
```

```javascript
const removeAllTodos = () => {
  todos.value = []
}
return {
  removeAllTodos,
}
```

![09-add-a-button-to-remove-all-todos](./assets/09-add-a-button-to-remove-all-todos.jpg)

## Beginning

```html
<template>
  <h1>Composition API</h1>
</template>

<script>
export default {
  setup() {

  }
}
</script>
```

## Add Fauna Query

```javascript
const faunadb = require('faunadb');

export const client = new faunadb.Client({ secret: 'FAUNA_KEY' })

const { Get, Ref, Collection } = faunadb.query;

export default {
  setup() {
    const faunaResponse = client.query(
      Get(
        Ref(
          Collection('Post'), '282918878459200013'
        )
      )
    )
    console.log("faunaResponse: ", '\n', '\n', faunaResponse)
  }
}
```

![00-01-faunaResponse](./assets/00-01-faunaResponse.jpg)

## Set postTitle to res.data.title

```javascript
const postTitle = faunaResponse.then(res => res.data.title)
console.log("postTitle: ", '\n', '\n', postTitle)
```

![00-02-postTitle](./assets/00-02-postTitle.jpg)

## Import ref

```javascript
import { ref } from 'vue'
```

## Set postTitle to postTitleRef with ref

```javascript
const postTitleRef = ref(postTitle)
console.log("postTitleRef: ", '\n', '\n', postTitleRef)
```

![00-03-postTitleRef](./assets/00-03-postTitleRef.jpg)

## Set postTitleValue with postTitleRef.value

```javascript
const postTitleValue = postTitleRef.value
console.log("postTitleValue: ", '\n', '\n', postTitleValue)
```

![00-04-postTitleValue](./assets/00-04-postTitleValue.jpg)

## Final

```html
<template>
  <h1>Composition API</h1>
</template>

<script>
const faunadb = require('faunadb');

export const client = new faunadb.Client({ secret: 'FAUNA_KEY' })

const { Get, Ref, Collection } = faunadb.query;

import { ref } from 'vue'

export default {
  setup() {
    const faunaResponse = client.query(
      Get(
        Ref(
          Collection('Post'), '282918878459200013'
        )
      )
    )
    console.log("faunaResponse: ", '\n', '\n', faunaResponse)

    const postTitle = faunaResponse.then(res => res.data.title)
    console.log("postTitle: ", '\n', '\n', postTitle)

    const postTitleRef = ref(postTitle)
    console.log("postTitleRef: ", '\n', '\n', postTitleRef)

    const postTitleValue = postTitleRef.value
    console.log("postTitleValue: ", '\n', '\n', postTitleValue)
  }
}
</script>
```
