<script>
// give each todo a unique id
let id = 0

export default {
  data() {
    return {
      newTodo: '',
      todos: [
        { id: id++, text: 'Learn HTML', finished:false},
        { id: id++, text: 'Learn JavaScript', finished:false},
        { id: id++, text: 'Learn Vue', finished:false}
      ]
    }
  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo, finished:false})
      this.newTodo = ''
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo)
    }
  }
}
</script>

<template>
    <div>
        <h1>Todo List</h1>
        <form @submit.prevent="addTodo">
            <v-text-field v-model="newTodo" id="newTodo"
                label="New todo"
                solo
            ></v-text-field>
            <v-btn @click="addTodo" id="addButton"
                color="#C70039"
                elevation="2"
                outlined
                icon
            >
                <v-icon>mdi-plus</v-icon>
            </v-btn>
        </form>

        

        <ul>
            <li v-for="todo in todos" :key="todo.id">
            {{ todo.text }}
            <v-btn @click="removeTodo(todo)"
                color="#8c1919"
                elevation="2"
                tile
                icon
            >
                <v-icon>mdi-close-thick</v-icon>
            </v-btn>
            </li>
        </ul>
    </div>
 </template>

 <style>
    body {
        background-color: #ffc4c4;
        margin: 5em;
    }

    div {
        align-items: center;
        display: flex;
        flex-direction: column;
    }

    form {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        margin: 1em;
    }

    #newTodo {
        width: 6em;

    }

    #addButton {
        margin-left: 2em;
    }

 </style>
 