<template>
  <p :class="['todo-item', todoProps.completed ? 'is-completed' : '']">
    <input type="checkbox" :checked="todoProps.completed" @change="markItemCompleted"/>
    {{ todoProps.title }}
    <button class="btn-del" @click="deleteItem">Delete</button>
  </p>
</template>
<script>

export default {
  name: 'TodoItem',
  props: ['todoProps'],
  setup(props, context) {
    const markItemCompleted = () => {
      context.emit('item-completed', props.todoProps.id)
    }

    const deleteItem = () => {
      context.emit('item-deleted', props.todoProps.id)
    }

    return {
      markItemCompleted,
      deleteItem
    }
  }
}
</script>
<style scoped>
.btn-del{
  background: red;
  cursor: pointer;
  color: white;
  float: right;
  border: none;
}
.todo-item{
  background: #f4f4f4;
  padding: 10px;
  margin: 0;
  border-bottom: 1px dotted #ccc;
}

.is-completed{
  text-decoration: line-through;
}
</style>