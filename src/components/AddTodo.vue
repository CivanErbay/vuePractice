<template>
    <div>
        <form @submit="addTodo">
            <input type="text" name="title" v-model="title" placeholder="Add Todo...">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
/* import { v4 as uuidv4 } from 'uuid';*/
export default {
    name: 'AddTodo',
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault(); //Because we dont the form to submit to a file
            const newTodo = {
                id: Math.floor(Math.random()*1000),
                title: this.title,
                completed: false
            }
            //Send up to parent $emit is always used when firing up to parent components
            this.$emit('add-todo', newTodo);

            this.title = '';
        }
    }
}
</script>

<style scoped>
form {
    display: flex;
}

input[type="text"] {
    flex: 10;
    padding: 5px;
}
</style>