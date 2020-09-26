<template>
<h1>Vue 3 Todo App</h1>
<form @submit.prevent="addNewTodo">
    <label for="">new todo</label> <br />
    <input v-model="newTodo" type="text" name="" id="" />
    <button>add new todo</button>
</form>

<ul v-for="(todo, index) in todos" :key="todo.id">
    <li @click="toggleDone(todo)" :class="{ done: todo.done }">
        {{ todo.content }}
        <button @click="removeTodo(index)">remove todo</button>
    </li>
</ul>
<button @click="removeAllTodo">Remove All Todo</button>
</template>

<script>
import {
    ref
} from 'vue';

export default {
    setup() {
        const newTodo = ref('');
        const todos = ref([]);

        function addNewTodo() {
            todos.value.push({
                done: false,
                content: newTodo.value,
            });
            newTodo.value = '';
        }

        function toggleDone(todo) {
            todo.done = !todo.done;
        }

        function removeTodo(index) {
            todos.value.splice(index, 1);
        }

        function removeAllTodo() {
            todos.value = [];
        }

        return {
            newTodo,
            todos,
            addNewTodo,
            toggleDone,
            removeTodo,
            removeAllTodo,
        };
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

.done {
    text-decoration: line-through;
}
</style>
