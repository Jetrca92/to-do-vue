<script setup>
    
</script>

<template>
    <header class="header">
        <div class="title-container">      
            <img alt="check icon" class="title-img" src="../assets/cb84809e138503e15457.png">
            <h2 class="h2">
                <span class="blue">To</span>
                <span class="blue-light">Do</span>
                <span class="gray">by Jetrca</span>
            </h2>
        </div>
        <div class="btn-container">
            <button class="btn btn-sm btn-outline-primary mx-1" id="inbox">Inbox</button>
            <button class="btn btn-sm btn-outline-primary mx-1" id="today">Today</button>
            <button class="btn btn-sm btn-outline-primary mx-1" id="upcoming">Upcoming</button>
            <button class="btn btn-sm btn-outline-primary mx-1" id="addTask">+ Add Task</button>
        </div>
    </header>
    <hr>
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