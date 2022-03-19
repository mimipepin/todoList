<script>
let id = 0;
export default {
  data() {
    return {
        hide: false,
        newTodo: '',
        todos: []
    }
  },
  mounted() {
      for(let i = 0; i < localStorage.length; i++) {
          this.todos.push({text: localStorage.key(i), finished: localStorage.getItem(localStorage.key(i))})
      }
  },
  computed: {
    filteredTodos() {
        return this.hide ? this.todos.filter((t) => !t.finished) : this.todos
    }
  },
  methods: {
    addTodo() {
        this.todos.push({ id: id++, text: this.newTodo, finished:false})
        localStorage.setItem(this.newTodo, false)
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
            <v-text-field v-model="newTodo"
                label="New todo"
                solo
            ></v-text-field>
            <v-btn @click="addTodo" id="addButton"
                color="#C70039"
                outlined
                icon
            >
                <v-icon>mdi-plus</v-icon>
            </v-btn>
        </form>

        <div v-if="filteredTodos.length > 0">
            <v-list>
                <v-list-item-group max-width="1000">
                    <v-list-item v-for="(item,i) in filteredTodos" :key=i>
                        <v-list-item-icon>
                            <v-icon color="#8c1919" @click="removeTodo(item)">mdi-close-thick</v-icon>
                        </v-list-item-icon>
                        <v-list-item-content>
                            <v-list-item-title @click="item.finished = !finished"> <span :class="{done: item.finished}">{{ item.text }}</span></v-list-item-title>
                        </v-list-item-content>
                        <v-list-item-action>
                            <v-checkbox v-model="item.finished"></v-checkbox>
                        </v-list-item-action>
                    </v-list-item>
                </v-list-item-group>
            </v-list>
        </div>
        <div v-else>
            <p id="noTasks">Congratulations, you completed all your tasks !</p>
        </div>
         <div id="hideButton">  
            <v-btn
                @click="hide = !hide"
                elevation="4"
                color="#F08080"
            >
                {{ hide ? "Show all" : "Hide completed" }}
            </v-btn>
        </div>
    </div>
 </template>

 <style>
    body {
        background-color: #feb1b1;
        margin: 5em;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    h1 {
        text-align: center;
        color: #C70039 ;
    }
    
    form {
        display: flex;
        flex-direction: row;
        margin: 1em;
    }

    #addButton {
        margin-left: 2em;
        margin-top: 0.5em;
    }

    .done {
        text-decoration: line-through;
    }

    #noTasks {
        color: #C70039;
    }

    #hideButton {
        margin-top: 2em;
        display: flex;
        flex-direction: column;
        align-items: center;
    }


 </style>
 