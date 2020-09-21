<template>
    <div>
        <div v-for="todo in todos" v-bind:key="todo.id"> <!-- :key property is necessary to bind iterations -->
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" /> <!-- @click="$emit('del-todo', todo.id)" -> This fires 'del-todo' to the parent -->
        </div>
    </div>
</template>

<script>
import TodoItem from './TodoItem'

export default {
    name: "Todos", //component Name which will be used for Export
    components: {
        TodoItem
    },
    props: ["todos"]
}
</script>

<style scoped>

</style>