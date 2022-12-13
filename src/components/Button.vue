<template>
    <button :class="addTaskToggle ? 'btn btn-danger rounded-1 btn-sm' : 'btn btn-success rounded-1 btn-sm'"
        @click="onToggle">{{ addTaskToggle ? 'Cancle' : 'Add Task' }}</button>
</template>
<script>
export default {
    name: "Button",
    props: {
        addTaskToggle: Boolean
    },
    methods: {
        onToggle() {
            this.$emit('add-task-toggle')
        }
    }
}
</script>