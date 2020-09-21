<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addTodo" /> <!-- v-on:add-todo catches the $emitted value from the AddTodo Component (Child) -->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/> <!-- second "todos" is referring to the todos in the data() -v-on is waiting for del-todo from children -->
  </div>
</template>

<script>

import Todos from './components/Todos'
import Header from './components/layout/Header'
import AddTodo from './components/AddTodo'

export default {
  name: "App",
  components: {
    Todos,
    Header,
    AddTodo
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
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo]
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

 .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>
