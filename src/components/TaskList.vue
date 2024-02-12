<script setup>
import { defineProps, onMounted } from 'vue'
const props = defineProps({
    task: Object
})

onMounted(() => {
    const dropdownToggleList = document.querySelectorAll('.dropdown-toggle');
    
    // Iterate over each dropdown toggle
    dropdownToggleList.forEach(dropdownToggle => {
        dropdownToggle.addEventListener('click', function () {
            const parent = this.closest('.dropdown');
            const dropdownMenu = parent.querySelector('.dropdown-menu');
            
            // Toggle class to show/hide dropdown menu
            dropdownMenu.classList.toggle('show');
        });
    });
})
</script>

<template>
    <li class="list-group-item">
        <div class="task-item" style="text-decoration: none;">
            <div class="list-checkmark me-3">
                <img class="unchecked-btn clickable" src="../assets/cb84809e138503e15457.png" alt="check icon">
            </div>
            <div class="list-content">
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
                            <a class="dropdown-item" href="#">Delete Task</a>
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
</style>
