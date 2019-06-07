<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Header from './components/layout/Header.vue';
import AddTodo from './components/AddTodo.vue';
import Todos from './components/Todos.vue';
import axios from 'axios';


export default {
  name: 'app',
  components: {
    Header,
    AddTodo,
    Todos
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete('https://jsonplaceholder.typicode.com/todos/${id}')
        .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(err => console.log(err));
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, newTodo])
        .catch(err => console.log(err));
      
    },
    
  
  },
   created() {
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(res => this.todos = res.data)
        .catch(err => console.log(err));
    }
}
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

  #app {
    width: 800px;
    margin: 0 auto;
  }

  .btn {
    display: inline-block;
    border: none;
    background: rgb(3, 59, 11);
    color: #fff;
    font-size: 16px;
    padding: 10px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: rgb(10, 92, 65);
  }
</style>
