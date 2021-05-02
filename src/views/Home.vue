<template>
    <div>
        <AddTask v-if="showAddTask" @add-task="addTask" />
    
        <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
    </div>
</template>

<script>
    import Tasks from '../components/Tasks'
    import AddTask from '../components/AddTask'

    export default {
        name: 'Home',

        props: {
            showAddTask: Boolean,
        },

        components: {
            Tasks,
            AddTask,
        },

        data() {
            return {
                tasks: [],
            }
        },
        
        methods: {
            async addTask(task) {
                const res = await fetch('api/tasks', {
                    method: 'POST',
                    headers: { 'Content-type': 'application/json' },
                    body: JSON.stringify(task)
                });
                const data = await res.json();
                this.tasks = [...this.tasks, data];
            },

            async deleteTask(id) {
                if (confirm('Are you sure you want to delete this task?')) {
                    const res = await fetch(`api/tasks/${id}`, {
                        method: 'DELETE',
                    });

                    if (res.status === 200){
                        this.tasks = this.tasks.filter(task => task.id !== id);
                    } else {  
                        return alert('Error deleting the current task...');
                    }
                }
            },

            async toggleReminder(id) {
                const toggleTask = await this.fetchTask(id);
                const updatedTask = { ...toggleTask, reminder: !toggleTask.reminder };

                const res = await fetch(`api/tasks/${id}`, {
                    method: 'PATCH',
                    headers: { 'Content-type': 'application/json' },
                    body: JSON.stringify(updatedTask),
                });

                const data = await res.json();

                this.tasks = this.tasks.map((task) => task.id === id ? { ...task, reminder: data.reminder } : task );
            },

            async fetchTasks() {
                const res = await fetch('api/tasks');
                const data = res.json();

                return data;
            },

            async fetchTask(id) {
                const res = await fetch(`api/tasks/${id}`);
                const data = res.json();

                return data;
            },

        },

        async created() {
            this.tasks = await this.fetchTasks();
        }

    }
</script>