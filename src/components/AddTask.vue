<template>
    <form @submit="submitTask" class="add-form">

        <div class="form-control">
            <label for="task">Task</label>
            <input type="text" v-model="text" name="text" placeholder="Add Task" />
        </div>

        <div class="form-control">
            <label for="day">Day and Time</label>
            <input type="text" v-model="day" name="day" placeholder="Add Day and Time" />
        </div>

        <div class="form-control form-control-check">
            <label for="reminder">Set Reminder</label>
            <input type="checkbox" v-model="reminder" name="reminder" />
        </div>

        <input type="submit" value="Save Task" class="btn btn-block" />
        
    </form>
</template>

<script>
    export default {
        name: 'AddTask',

        data() {
            return {
                text: '',
                day: '',
                reminder: false
            }
        },

        methods: {
            submitTask(e) {
                // Do not refresh the browser
                e.preventDefault();

                if (!this.text || !this.day) {
                    return alert('Please fill all fields to add a task');
                }

                // Generate random ID
                // const randomId = Math.floor(Math.random() * 100000 + 1);

                // Create new task object
                const newTask = {
                    // id: randomId,
                    text: this.text,
                    day: this.day,
                    reminder: this.reminder,
                }

                this.$emit('add-task', newTask);

                this.text = '';
                this.day = '';
                this.reminder = false;
            }
        }
    }
</script>

<style scoped>

    .add-form {
        margin-bottom: 40px;
        animation: slideIn .4s ease-in;
    }

    @keyframes slideIn {
        0% {
            opacity: 0;
            transform: translateY(-50px);
        }

        100% {
            opacity: 1;
            transform: translateY(0);
        }
    }

    .form-control {
        margin: 20px 0;
    }

    .form-control label {
        display: block;
    }

    .form-control input {
        width: 100%;
        height: 40px;
        margin: 5px;
        padding: 3px 7px;
        font-size: 17px;
    }

    .form-control-check {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .form-control-check label {
        flex: 1;
    }

    .form-control-check input {
        flex: 2;
        height: 20px;
    }
</style>