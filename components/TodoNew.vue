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
  </div>
</template>

<script>
export default {
  name: 'TodoNew',
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
  },
  mounted() {
    this.$emit('new-data', this.todos)
  },
}
</script>
