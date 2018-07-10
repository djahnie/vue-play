<template>
  <div id="app">
    <h2>{{ title }}</h2>
    <todo-list />
    <input type="text" v-model="newTodoText" />
    <!-- value sets the text inside the input field, :value makes it expect js which means it can put it in a variable -->
    <!-- v-model makes a two-way-data-binding so that newTodoText in data can be overwritten -->
    <button @click="addTodo">New todo</button> <!-- what's actually written here is this.addTodo(), but vue adds that for us -->
  </div>
</template>

<script>
import TodoList from './components/TodoList'

export default {
  name: 'app',
  components: {
    TodoList
  },
  data: function() {
    return {
      title: "Todo List",
      newTodoText: 'new item' // data only has the initial value specified in here
    }
  },
  methods: {
    addTodo: function() {      
      this.todos.push(this.newTodoText) //one component is like a room, and 'this' help us to find variables on other tables
    }
  }
}
</script>
