<template>
  <form @submit="addItem">
    <input type="text" placeholder="add job" v-model.trim="title" />
    <button class="add-btn">Add Todo</button>
  </form>
</template>
<script>
import { ref } from '@vue/reactivity'
import { v4 as uuidv4 } from 'uuid'

export default {
  name: 'Add Todo',
  setup(props, context) {
    const title = ref('')
    const addItem = e => {
      e.preventDefault()
      const newItem = {
        id: uuidv4(),
        text: title.value,
        completed: false
      }
      context.emit('adNewTodo', newItem)
      title.value = ''
    }
    return {
      title,
      addItem
    }
  }
}
</script>
<style scoped>
form {
  display: flex;
}
input[type='text'] {
  flex: 10;
  padding: 10px 5px;
  outline: none;
}
button {
  flex: 2;
  padding: 10px 5px;
  outline: none;
}
</style>
