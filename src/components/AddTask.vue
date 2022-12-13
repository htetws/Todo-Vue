<template>
    <form @submit.prevent="addTask" class="px-3" method="post">
        <div class="form-group mt-4">
            <label class="mb-1">Task</label>
            <input v-model="task" type="text" class="form-control rounded-1" placeholder="Enter Task ...">
            <small class="text-danger" v-show="taskStatus">Need To Fill Task !</small>
        </div>
        <div class="form-group mt-4">
            <label class="mb-1">Day & Time</label>
            <input v-model="time" type="text" class="form-control rounded-1" placeholder="Enter Day & Time ...">
            <small class="text-danger" v-show="timeStatus">Need To Fill Time !</small>
        </div>
        <div class="form-group mt-4">
            <label class="mb-1 me-5">Add Reminder</label>
            <input v-model="reminder" type="checkbox" class="form-check-input">
        </div>
        <input type="submit" value="Save Task" class="btn btn-dark w-100 my-3" />
    </form>
</template>

<script>
export default {
    name: "AddTask",
    data: () => {
        return {
            taskStatus: false,
            timeStatus: false,
            task: '',
            time: '',
            reminder: false
        }
    },
    methods: {
        addTask() {
            this.emptyCheck()
            if (!this.taskStatus && !this.timeStatus) {

                this.$emit('add-task-data', {
                    id: Math.floor(Math.random() * 100000),
                    title: this.task,
                    time: this.time,
                    reminder: this.reminder
                })

                this.clearField()
            }
        },
        emptyCheck() {
            this.taskStatus = this.task === "" ? true : false
            this.timeStatus = this.time === "" ? true : false
        },
        clearField() {
            this.task = ''
            this.time = ''
            this.reminder = false
        }
    }
}
</script>

<style scoped>
input:focus {
    box-shadow: none !important;
}
</style>