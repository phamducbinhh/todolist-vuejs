<template>
  <AddTodo v-on:adNewTodo="addItem" />
  <TodoItem
    v-for="todo in array"
    :key="todo.id"
    :todoProps="todo"
    @todoItemComplete="handleClick"
    @todoItemRemove="handleDelete"
  >
    {{ todo }}
  </TodoItem>
</template>
<script>
import { ref } from '@vue/reactivity'
import TodoItem from './TodoItem.vue'
import AddTodo from './AddTodo.vue'
export default {
  name: 'Todos',
  setup() {
    const todos = ref([
      {
        id: 1,
        text: 'Learn React',
        completed: false
      },
      {
        id: 2,
        text: 'Learn Vuejs',
        completed: false
      },
      {
        id: 3,
        text: 'Learn AngularJS',
        completed: false
      }
    ])

    const handleClick = id => {
      todos.value.map(item => {
        item.id === id ? (item.completed = !item.completed) : ''
        return item
      })
    }

    const handleDelete = id => {
      todos.value = todos.value.filter(item => {
        return item.id !== id
      })
    }

    const addItem = newTodo => {
      todos.value.push(newTodo)
    }
    return {
      array: todos,
      handleClick,
      handleDelete,
      addItem
    }
  },
  components: { TodoItem, AddTodo }
}
</script>
<style scoped></style>
