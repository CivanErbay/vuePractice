<template>
    <div>
        <div v-for="todo in todos" :key="todo.id"> <!-- :key property is necessary to bind iterations -->
            <h3>{{todo.title}}</h3>
        </div>
    </div>
</template>

<script>
export default {
    name: "Todos", //component Name which will be used for Export
    props: ["todos"]
}
</script>

<style scoped>

</style>