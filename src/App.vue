<template>
  <div id="app">
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/> <!-- second "todos" is referring to the todos in the data() -v-on is waiting for del-todo from children -->
  </div>
</template>

<script>

import Todos from './components/Todos'

export default {
  name: "App",
  components: {
    Todos
  },
  data() {
    return {
      todos:
     [
       {
         id: 1,
         title: "Todo One",
         completed: true
       },{
         id: 2,
         title: "Todo Two",
         completed: true
       },{
         id: 3,
         title: "Todo Three",
         completed: false
       },
     ]
    };
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id); //gives back all the todos where the id is NOT the one, which is clicked --> returns an array of todos except the clicked one
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
