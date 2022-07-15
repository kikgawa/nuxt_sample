<template>
  <div>
    <v-form @submit.prevent="addTask">
      <v-layout row align-center x1>
        <v-flex sm10 pa-2>
          <v-text-field v-model="newTodo"></v-text-field>
        </v-flex>
        <v-flex sm2 pa-2>
          <v-btn type="submit">追加</v-btn>
        </v-flex>
      </v-layout>
    </v-form>
    <ul>
      <li v-for="(todo, index) in todos">
        {{ todo.item }}
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
export default {
  name: 'TodoPage',
  data() {
    return {
      newTodo: '',
      todos: [],
    }
  },
  methods: {
    addTask() {
      if (this.newTodo === '') return
      let todo = {
        item: this.newTodo,
        isActive: false,
      }
      this.todos.push(todo)
      this.newTodo = ''
    },
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
