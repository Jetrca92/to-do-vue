<template>
	<NavBar />
	<ul class="list-group">
		<TaskList
			v-for="(task, index) in taskList"
			:key="index"
			:task="task"
			:taskList="taskList"
			:deleteTask="deleteTask"
		></TaskList>
	</ul>
</template>
	
<script setup>
import { ref } from 'vue'
import NavBar from "./components/NavBar"
import TaskList from "./components/TaskList"

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
</script>
