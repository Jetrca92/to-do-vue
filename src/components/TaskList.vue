<script setup>
import { defineProps } from 'vue'

const props = defineProps({
    task: Object,
    taskList: Array,
    deleteTask: Function,
})
const toggleCompleted = (task) => {
    task.completed = !task.completed
}
</script>

<template>
    <li class="list-group-item">
        <div class="task-item" style="text-decoration: none;">
            <div class="list-checkmark me-3">
                <img 
                    class="clickable"
                    :class="{ 'unchecked-btn': !props.task.completed, 'checked-btn': props.task.completed }"
                    src="../assets/cb84809e138503e15457.png" 
                    alt="check icon"
                    @click="toggleCompleted(props.task)"
                >
            </div>
            <div 
                class="list-content"
                :class="{ 
					strikeout: props.task.completed,
                }"
            >
                <div class="d-flex justify-content-between">
                    <div>
                        <b class="me-3">{{ props.task.name }}</b>
                        <span v-if="props.task.isUrgent">(Urgent)</span>
                    </div>
                    <div>
                        <span>{{ props.task.date }}</span>
                    </div>
                    <div class="dropdown btn-container">
                        <button class="btn btn-sm btn-outline-primary dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false">Delete</button>
                        <ul class="dropdown-menu">
                        <li>
                            <a
                                class="dropdown-item" 
                                href="#"
                                @click="props.deleteTask(props.task)"
                            >Delete Task</a>
                        </li>
                    </ul>
                    </div>
                </div>
            </div>
        </div>
    </li>
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

.strikeout {
    text-decoration: line-through;
}
</style>
