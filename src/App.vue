<template>
	<NavBar @toggle-add-task-form="toggleAddTaskForm"/>
	<ul class="list-group" v-if="!showAddTaskForm">
		<h2 class="h2"><span class="gray">All Tasks</span></h2>
		<TaskList
			v-for="(task, index) in taskList"
			:key="index"
			:task="task"
			:deleteTask="deleteTask"
		></TaskList>
	</ul>
	<AddTask
		@toggle-add-task-form="toggleAddTaskForm"
		v-if="showAddTaskForm"
		:createNewTask="createNewTask"
	></AddTask>
</template>
	
<script setup>
import { ref } from 'vue'
import NavBar from "./components/NavBar"
import TaskList from "./components/TaskList"
import AddTask from "./components/AddTask"

const today = new Date()
const taskList = ref([
	{ name: "Learn Vue!", date: today, isUrgent: false, completed: false },
	{ name: "Go for a run", date: today, isUrgent: true, completed: false },
])

const deleteTask = (task) => {
    const index = taskList.value.findIndex((item) => item === task);
    const updatedTaskList = taskList.value.filter((item, i) => i !== index);
    taskList.value = updatedTaskList;
}
const createNewTask = (taskName, date, taskUrgent) => {
	taskList.value.push({ name: taskName, date: date, isUrgent: taskUrgent, completed: false })
	showAddTaskForm.value = false
}
const showAddTaskForm = ref(false)
const toggleAddTaskForm = () => {
    showAddTaskForm.value = !showAddTaskForm.value;
}
</script>
