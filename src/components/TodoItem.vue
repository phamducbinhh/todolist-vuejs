<template>
  <p :class="['todo-item', todoProps.completed ? 'isComplete' : '']">
    <input
      type="checkbox"
      :checked="todoProps.completed"
      @click="handleClick"
    />
    {{ todoProps?.title }}
    <button class="del-btn" @click="handleDelete">Delete</button>
  </p>
</template>
<script>
export default {
  name: 'TodoItem',
  props: ['todoProps'],
  setup(props, context) {
    const handleClick = () => {
      context.emit('todoItemComplete', props.todoProps.id)
    }
    const handleDelete = () => {
      context.emit('todoItemRemove', props.todoProps.id)
    }
    return {
      handleClick,
      handleDelete
    }
  }
}
</script>
<style scoped>
.del-btn {
  background: #ff0000;
  color: #fff;
  border: none;
  cursor: pointer;
  float: right;
}
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  margin: 0;
  border-bottom: 1px solid #ccc;
}
.isComplete {
  text-decoration: line-through;
}
</style>
