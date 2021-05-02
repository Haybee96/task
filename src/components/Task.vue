<template>
    <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '' ,'task']">
        <h3>
            {{task.text}}
            <i @click="$emit('delete-task', id)" class="fas fa-times"></i>
        </h3>
        <p>{{task.day}}</p>
    </div>
</template>

<script>
    export default {
        name: 'Task',
        props: {
            task: Object,
        },
    }
</script>

<style scoped>

    .fas {
        color: red;
    }
    .task {
        background: #f4f4f4f4;
        margin: 5px;
        padding: 10px 20px;
        cursor: pointer;
        animation: scaleIn .4s ease-in;
    }

    @keyframes scaleIn {
        0% {
            opacity: 0;
            transform: scale(0);
        }

        100% {
            opacity: 1;
            transform: scale(1);
        }
    }

    .task.reminder {
        border-left: 5px solid green;
    }

    .task h3 {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>