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

        <v-list>
            <v-list-item-group max-width="1000">
                <v-list-item v-for="item in todos" :key="item.id">
                    <v-list-item-icon>
                        <v-icon color="#8c1919" @click="removeTodo(item)">mdi-close-thick</v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>
                        <v-list-item-title v-text="item.text"></v-list-item-title>
                    </v-list-item-content>
                    <v-list-item-action>
                        <v-checkbox ></v-checkbox>
                    </v-list-item-action>
                </v-list-item>
            </v-list-item-group>
        </v-list>
    </div>
 </template>

 <style>
    body {
        background-color: #ffc4c4;
        margin: 5em;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    
    div {
    }
    
    form {
        display: flex;
        flex-direction: row;
        margin: 1em;
    }

    #newTodo {
        width: 6em;

    }

    #addButton {
        margin-left: 2em;
    }



 </style>
 