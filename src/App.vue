<template>
  <div id="app">
    <h2>{{ title }}</h2>
    <ul>
      <li v-for="(item, index) in todos" :key="index"> <!-- the key needs to be specified for everything to be proper and not use ambiguous keys-->
        <list-item 
          :title="item"
          @textEdited='grabEditedText(index, arguments[0])'
          @itemDeleted='getRidOfIt(index)' /> 
        <!-- the event 'textEdited' calls the function 'grabEditedText' -->
        <!-- grabEditedText has two arguments from two different spaces: index from the v-for the line above, and arguments[0] from the $emit in ListItem -->
        <!-- the 'arguments' arg exists in every js function and is a kinda magical cheating thing -->
        <!-- and _actually_ we don't call a function here (cause that doesn't work in the template), but reference a function that will then be called in the script -->
      </li>
    </ul>
    <input type="text" v-model="newTodoText" />
    <!-- value sets the text inside the input field, :value makes it expect js which means it can put it in a variable -->
    <!-- v-model makes a two-way-data-binding so that newTodoText in data can be overwritten -->
    <button @click="addTodo">New todo</button> <!-- what's actually written here is this.addTodo(), but vue adds that for us -->
  </div>
</template>

<script>
import ListItem from './components/ListItem'

export default {
  name: 'app',
  components: {
    ListItem, // would be ListItem: ListItem if the names were different,
  },
  data: function() {
    return {
      title: 'Todo list', // variable that is used in the h2, just to 
      todos: ['first thing', 'second thing', 'many more things...'],
      newTodoText: 'new item', // data only has the initial value specified in here
    }
  },
  methods: {
     addTodo: function() {      
        this.todos.push(this.newTodoText) //one component is like a room, and 'this' help us to find variables on other tables
      },
      grabEditedText: function(index, newtext) { // the two parameters are those passed on in 'submitEditedText'
        // this.todos[this.todos.indexOf(oldtext)] = newtext // was supposed to put the new text where the old text was in the array 'todos'
        // BUT: vue doesn't notice when there's changes in a prop so it doesn't automatically reload
        // https://vuejs.org/v2/guide/reactivity.html#ad
        this.$set(this.todos, index, newtext)
        // every function needs to be prefixed with 'this', because also the internal ones are specified inside the individual files
      },
      getRidOfIt: function(index) {
        console.log(index)
        this.$delete(this.todos, index) // $delete takes (object, key) arguments
      }
  },
}
</script>
