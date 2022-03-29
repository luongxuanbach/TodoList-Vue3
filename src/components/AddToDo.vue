<template>
  <form @submit="addItem">
    <input type="text" placeholder="New todo" v-model="title" />
    <input type="submit" value="Add" class="add-btn"/>
  </form>
</template>
<script>
import { ref } from 'vue'
import {v4 as uuid} from 'uuid'

export default {
    name: 'AddToDo',
    setup(props, context) {
      const title = ref('')

      const addItem = (event) => {
        event.preventDefault()
        const newItem = {
          id: uuid,
          title: title.value,
          completed: false
        }

        context.emit('add-todo', newItem)

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
form{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
input[type="text"]{
  flex: 10;
  padding: 5px;
}

input[type="submit"]{
  flex: 2;
}
</style>