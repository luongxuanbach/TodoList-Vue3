<template>
  <AddTodo
      @add-todo="addTodo"
  />
  <TodoItem v-for="todo in todos"
            :key="todo.id"
            :todoProps="todo"
            @item-completed="markCompleted"
            @item-deleted="deleteItem"
  />
</template>

<script>
import {ref} from "vue";
import TodoItem from "@/components/TodoItem";
import AddTodo from "@/components/AddToDo";
import axios from "axios";

export default {
  name: 'Todo-item',
  components: {TodoItem, AddTodo},
  setup() {
    const todos = ref([])

    const getAllTodos = async () => {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10');
        todos.value = response.data;
      } catch (error) {
        console.log(error);
      }

    }

    const markCompleted = (id) => {
      todos.value.forEach(todo => {
        if (todo.id === id) {
          todo.completed = !todo.completed
        }
      })
    }

    const deleteItem = async (id) => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
        todos.value = todos.value.filter(todo => todo.id !== id);
      } catch (error) {
        console.log(error);
      }
    }

    const addTodo = (newItem) => {
      todos.value.push(newItem)
    }

    getAllTodos()
    return {
      todos,
      markCompleted,
      deleteItem,
      addTodo,
    }
  }
}
</script>
<style scoped>
p {
  color: black;
}
</style>