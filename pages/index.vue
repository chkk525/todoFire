
<template lang="html">
  <div id="todo">
    <input v-model="todoText" type="text" @keyup.enter="addTodo">

    <li v-for="todo in todos" :key="todo['.key']">
      {{ todo['.value'] }}
      <button @click="removeTodo(todo['.key'])">
        X
      </button>
    </li>
  </div>
</template>

<script>
import { ADD_TODO, REMOVE_TODO, INIT_TODO } from '../store/action-types'
export default {
  data() {
    return {
      todoText: ''
    }
  },
  computed: {
    todos() {
      return this.$store.getters.getTodos
    }
  },
  created() {
    this.$store.dispatch(INIT_TODO)
  },
  methods: {
    addTodo() {
      this.$store.dispatch(ADD_TODO, this.todoText)
      this.todoText = ''
    },
    removeTodo(key) {
      this.$store.dispatch(REMOVE_TODO, key)
    }
  }
}
</script>

<style lang="css">
</style>
