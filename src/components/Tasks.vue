<template>
    <div class="mt-4">
        <div v-if="tasks.length > 0">
            <div title="Double Click to Done Task." @dblclick="$emit('toggle-task', task.id)" v-for="task in tasks"
                :key="task.id"
                :class="task.reminder ? 'border-start border-5 border-success bg-light shadow-sm col-12 p-3 mt-2' : 'bg-light shadow-sm col-12 p-3 mt-2'">
                <Task @task-delete="$emit('task-delete', task.id)" :task="task" />
            </div>
        </div>
        <div v-else class="text-center shadow-sm p-3">! Oops, no data found. Let's create new task first.</div>
    </div>

</template>
<script>
import Task from './Task.vue';
export default {
    name: "Tasks",
    props: {
        tasks: Array,
    },
    components: {
        Task
    },
    emits: ['task-delete', 'toggle-task']
}
</script>