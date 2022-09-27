<template>
  <AddTodo v-on:adNewTodo="addItem" />
  <TodoItem
    v-for="todo in todos"
    :key="todo.id"
    :todoProps="todo"
    @todoItemComplete="handleClick"
    @todoItemRemove="handleDelete"
  >
    {{ todo }}
  </TodoItem>
  <div class="btn-remove-all">
    <button class="btn-all" @click="handleRemoveAll">Delete All</button>
  </div>
</template>
<script>
import { ref } from '@vue/reactivity'
import TodoItem from './TodoItem.vue'
import AddTodo from './AddTodo.vue'
import axios from 'axios'
export default {
  name: 'Todos',
  setup() {
    const todos = ref([])
    const getAllTodos = async () => {
      try {
        const respones = await axios.get(
          `https://jsonplaceholder.typicode.com/todos?_limit=5`
        )
        if (respones && respones.data) {
          todos.value = respones.data
        }
      } catch (err) {
        alert(err.message)
      }
    }
    getAllTodos()
    const handleClick = id => {
      todos.value.map(item => {
        item.id === id ? (item.completed = !item.completed) : ''
        return item
      })
    }

    const handleDelete = async id => {
      try {
        const res = await axios.delete(
          `https://jsonplaceholder.typicode.com/todos/${id}`
        )
        console.log(res.data)
        todos.value = todos.value.filter(item => {
          return item.id !== id
        })
      } catch (err) {
        console.log(err.message)
      }
    }

    const addItem = async newTodo => {
      try {
        const res = await axios.post(
          'https://jsonplaceholder.typicode.com/todos',
          newTodo
        )
        if (newTodo.title == '') return
        todos.value.push(res.data)
      } catch (err) {
        console.log(err.message)
      }
    }

    const handleRemoveAll = () => {
      todos.value = []
    }
    return {
      todos,
      handleClick,
      handleDelete,
      addItem,
      handleRemoveAll
    }
  },
  components: { TodoItem, AddTodo }
}
</script>
<style scoped>
.btn-remove-all {
  width: 100%;
  display: flex;
  justify-content: center;
  margin-top: 20px;
}
.btn-all {
  padding: 10px 30px;
  background-color: orange;
  border: 0;
}
</style>
