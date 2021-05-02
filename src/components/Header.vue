<template>
    <header>
        <h1>{{ title }}</h1>
        <Button @btn="$emit('toggle-add-task-form')" :text="addTask ? 'Close' : 'Add Task'" :color="addTask ? 'orangered' : 'green'" />
    </header>
</template>

<script>
    import Button from './Button'

    export default {
        name: 'Header',

        props: {
            title: String,
            addTask: Boolean,
        },

        components: {
            Button,
        },
    }
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>