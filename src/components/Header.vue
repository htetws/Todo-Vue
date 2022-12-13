<template>
    <div class="d-flex justify-content-between align-items-center ">
        <span class="fs-4 fw-bold">{{ title }}</span>

        <div class="form-group">
            <label class="me-2">Done</label>
            <input type="checkbox" class="form-check-input" v-model="hideDoneStatus"
                @change="$emit('hide-done-task', hideDoneStatus)" />
        </div>

        <Button :addTaskToggle="addTaskToggle" @add-task-toggle="$emit('add-task-toggle')" />
    </div>
</template>
<script>
import Button from './Button.vue';
export default {
    name: "Header",
    data: () => {
        return {
            hideDoneStatus: false
        }
    },
    props: {
        title: String,
        addTaskToggle: Boolean,
    },
    components: {
        Button
    },
    emits: ['add-task-toggle', 'hide-done-task']
}
</script>