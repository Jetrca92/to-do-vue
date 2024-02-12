<template>
	<NavBar />
	<ul class="list-group">
		<TaskList
			v-for="(task, index) in taskList"
			:key="index"
			:task="task"
		></TaskList>
	</ul>
</template>
	
<script setup>
import { ref } from 'vue'

import NavBar from "./components/NavBar"
import TaskList from "./components/TaskList"
const today = new Date()
const taskList = ref([
	{ name: "Learn Vue!", date: today, isUrgent: false },
	{ name: "Go for a run", date: today, isUrgent: true },
])
</script>