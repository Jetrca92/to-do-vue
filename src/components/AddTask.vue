<script setup>
import { ref, defineProps, defineEmits, computed } from 'vue'

const emit = defineEmits(['toggle-add-task-form']);
const toggleAddTaskForm = () => {
    emit('toggle-add-task-form');
};

const props = defineProps({
    createNewTask: Function,
})
const taskName = ref('')
const date = ref('')
const taskUrgent = ref(false)
const isFormInvalid = computed(() => {
    return !taskName.value || !date.value
})
</script>
<template>
    <h2 class="h2"><span class="gray">Add Task</span></h2>
    <form id="form">
        <div class="mb-3">
            <label for="task-name" class="form-label">Task name</label>
            <input 
                type="text" 
                class="form-control" 
                id="task-name"
                v-model="taskName"
                required
            >
        </div>
        <div class="mb-3">
            <label for="task-date" class="form-label">Date</label>
            <input 
                type="date" 
                class="date form-control" 
                id="task-date" 
                v-model="date"
                required
            >
        </div>
        <div class="mb-3 form-check">
            <input 
                type="checkbox" 
                class="form-check-input"
                v-model="taskUrgent" 
                id="task-urgent"
            >
            <label class="form-check-label" for="task-urgent">Check if task is urgent</label>
        </div>
        <div class="btn-container d-flex gap-3">
            <button 
                class="btn btn-sm btn-outline-primary"
                @click.prevent="props.createNewTask(taskName, date, taskUrgent)"
                :disabled="isFormInvalid"
            >Submit</button>
            <button 
                class="btn btn-sm btn-outline-primary"
                @click.prevent="toggleAddTaskForm"
            >Cancel</button>
        </div>
    </form>
</template>

<style scoped>
.btn-container .btn-outline-primary {
    color: #3D9AE2 !important;
    border-color: #3D9AE2 !important;
}

.btn-container .btn-outline-primary:hover {
    background-color: #3D9AE2 !important;
    border-color: #3D9AE2 !important;
    color: white !important;
}

.btn-container .btn-outline-primary:active {
    background-color: #3D9AE2 !important;
    border-color: #3D9AE2 !important;
}
</style>