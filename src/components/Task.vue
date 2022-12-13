<template>
    <div role="button" class="d-flex align-items-center justify-content-between">
        <h6 class="text-muted">{{ task.title }}</h6>
        <i class="fas fa-times text-danger fs-4" role="button" @click="$emit('task-delete', task.id)"></i>
    </div>
    <small>{{ task.time }}</small>
</template>

<script>
export default {
    name: "Task",
    props: {
        task: Object
    },
    emits: ['task-delete']
}
</script>

