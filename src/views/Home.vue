<template>
  <div id="app">

    <AddTodo v-on:add-todo="addTodo" />
    <!-- v-on:add-todo catches the $emitted value from the AddTodo Component (Child) -->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
    <!-- second "todos" is referring to the todos in the data() -v-on is waiting for del-todo from children -->
  </div>
</template>

<script>
import Todos from "../components/Todos";

import AddTodo from "../components/AddTodo";
import axios from "axios";

export default {
  name: "App",
  components: {
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(() => (this.todos = this.todos.filter((todo) => todo.id !== id))) //gives back all the todos where the id is NOT the one, which is clicked --> returns an array of todos except the clicked one
        .catch((err) => console.log(err));
    },

    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          //This Post-Request fires your custom todo.title and completed (false) and give back the same + the ID which jsonplaceholder creates for you
          title,
          completed,
        })
        .then((res) => this.todos = [...this.todos, res.data]) //equal to this.todos.push(res.data)
        .catch((err) => console.log(err));
    },
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((res) => {
        this.todos = res.data;
      })
      .catch((err) => console.log(err));
  },
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
