<script>

let id = 0

export default {
    data() {
        return {
            todos: [
                { id: id++, text: "don't worry"},
                { id: id++, text: "be happy"}
            ]
        }
    }
}
</script>

<template>
    <div>
        <h1>Salut, bienvenue sur ta Todo-List !</h1>
        <ul>
            <li v-for="todo in todos" :key="todo.id">
                {{ todo.text }}
            </li>
        </ul>

    </div>
 </template>