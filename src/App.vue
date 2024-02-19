<template>
	<NavBar 
		@toggle-state="toggleState"
	/>
	<div v-if="showIndex">
		<ul class="list-group">
		<h2 class="h2"><span class="gray">All Tasks</span></h2>
		<div v-if="taskList.length > 0">
			<TaskList
			v-for="(task, index) in taskList"
			:key="index"
			:task="task"
			:deleteTask="deleteTask"
			></TaskList>
		</div>
		<div v-else>
			No tasks.
		</div>
		</ul>
	</div>
	<div v-if="showToday">
		<ul class="list-group">
		<h2 class="h2"><span class="gray">Today's Tasks</span></h2>
		<div v-if="taskListToday.length > 0">
			<TaskList
				v-for="(task, index) in taskListToday"
				:key="index"
				:task="task"
				:deleteTask="deleteTask"
			></TaskList>
		</div>
		<div v-else>
			<p>No tasks for today.</p>
		</div>
		</ul>
	</div>
	<div v-if="showUpcoming">
		<ul class="list-group">
		<h2 class="h2"><span class="gray">Upcoming Tasks</span></h2>
		<div v-if="taskListUpcoming.length > 0">
			<TaskList
			v-for="(task, index) in taskListUpcoming"
			:key="index"
			:task="task"
			:deleteTask="deleteTask"
		></TaskList>
		</div>
		<div v-else>
			<p>No upcoming tasks.</p>
		</div>
		</ul>
	</div>
	<div v-if="showAddTaskForm">
		<AddTask
			@toggle-state="toggleState"
			v-if="showAddTaskForm"
			:createNewTask="createNewTask"
		></AddTask>
	</div>
</template>
	
<script setup>
// First time this
import { ref, computed } from 'vue'
import NavBar from "./components/NavBar"
import TaskList from "./components/TaskList"
import AddTask from "./components/AddTask"

const today = new Date()
const taskList = ref([
	{ name: "Learn Vue!", date: today, isUrgent: false, completed: false },
	{ name: "Go for a run", date: today, isUrgent: true, completed: false },
])
const filterTasksByDate = (date, upcoming = false) => {
    return taskList.value.filter(task => {
        if (upcoming) {
            return task.date > date;
        } else {
            return (
                task.date.getFullYear() === date.getFullYear() &&
                task.date.getMonth() === date.getMonth() &&
                task.date.getDate() === date.getDate()
            );
        }
    });
};
const taskListToday = computed(() => {
	return filterTasksByDate(today)
})
const taskListUpcoming = computed (() => {
	return filterTasksByDate(today, true)
})
const deleteTask = (task) => {
    const index = taskList.value.findIndex((item) => item === task);
    const updatedTaskList = taskList.value.filter((item, i) => i !== index);
    taskList.value = updatedTaskList;
}
const createNewTask = (taskName, date, taskUrgent) => {
	const dateObject = new Date(date)
	taskList.value.push({ name: taskName, date: dateObject, isUrgent: taskUrgent, completed: false })
	showAddTaskForm.value = false
	showIndex.value = true
}
const showAddTaskForm = ref(false)
const showIndex = ref(true)
const showToday = ref(false)
const showUpcoming = ref(false)
const toggleState = (state) => {
    showIndex.value = state === 'inbox'
	showToday.value = state === 'today'
	showUpcoming.value = state === 'upcoming'
	showAddTaskForm.value = state === 'addTask'
}
</script>
