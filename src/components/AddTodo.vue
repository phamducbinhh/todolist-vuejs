<template>
  <form @submit="addItem">
    <input type="text" placeholder="add job" v-model.trim="title" />
    <button class="add-btn">Add Todo</button>
  </form>
</template>
<script>
import { ref } from '@vue/reactivity'

export default {
  name: 'Add Todo',
  setup(props, context) {
    const title = ref('')
    const addItem = e => {
      e.preventDefault()
      const newItem = {
        title: title.value,
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
