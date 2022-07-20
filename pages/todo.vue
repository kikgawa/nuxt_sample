<template>
  <div>
    <TodoNew @new-data="newData($event, todos)"></TodoNew>

    <ul>
      <li v-for="(todo, index) in todos">
        <nuxt-link :to="`/edit/${index}`">
          {{ todo.item }}
        </nuxt-link>
        <span v-if="todo.isActive">
          <span>
            <input class="input" type="text" v-model="todo.item" key="edit" />
          </span>
          <button @click="updateTask(index)">確定</button>
        </span>
        <button v-show="!todo.isActive" @click="editTask(index)">編集</button>
        <button @click="deleteTask(index)">削除</button>
      </li>
    </ul>
  </div>
</template>

<script>
import Vue from 'vue'
import TodoNew from '~/components/TodoNew.vue'

export default {
  name: 'TodoPage',
  components: { TodoNew },
  data() {
    return {
      todos: [],
      title: 'Todo App',
    }
  },

  head() {
    return {
      title: this.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Todo App description',
        },
      ],
    }
  },
  methods: {
    deleteTask(index) {
      this.todos.splice(index, 1)
    },
    editTask(index) {
      this.todos[index].isActive = true
      this.todos[index].item = this.todos[index].item
    },
    updateTask(index) {
      this.todos[index].isActive = false
    },
    newData(todos) {
      this.todos = todos
    },
  },
}
</script>

<style scoped>
.input,
.input:focus {
  border: 1px solid #666;
  color: #ccc;
  margin: 0 10px;
  padding: 0 5px;
}
</style>
