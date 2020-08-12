<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <div class="info">Total Tasks: {{ done }} / {{ todos.length }}</div>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import axios from "axios";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";

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
        .then(() => {
          this.todos = this.todos.filter((todo) => todo.id !== id);
        })
        .catch((err) => console.log("Error: " + err));
    },
    addTodo(todo) {
      const { title, completed } = todo;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed,
        })
        .then((todo) => {
          this.todos = [...this.todos, todo.data];
        })
        .catch((err) => console.log("ERROR: " + err));
    },
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then((todos) => {
        this.todos = todos.data;
      })
      .catch((err) => console.log("error occured: " + err));
  },
  computed: {
    done() {
      const doneTasks = this.todos.filter((todo) => todo.completed);
      return doneTasks.length;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.info {
  display: flex;
  margin: 0.5rem 0;
  font-weight: 600;
}
</style>
