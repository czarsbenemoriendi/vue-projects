<script setup>
import { computed, reactive, ref, watch } from 'vue';

const task = ref('');
const tasks = reactive([]);
const addTask = () => {
	tasks.push(task.value);
};
const isActive = ref(true);
const hideList = () => {
	isActive.value = !isActive.value;
};
</script>
<template>
	<div>
		<header>
			<h1>Vue Lists and Conditional Content</h1>
		</header>
		<section id="assignment">
			<h2>Assignment</h2>
			<input type="text" v-model="task" />
			<button @click="addTask">Add Task</button>
			<ul v-show="isActive">
				<li v-for="task in tasks">{{ task }}</li>
			</ul>
			<button @click="hideList">{{ isActive ? 'Hide' : 'Show' }}</button>
		</section>
	</div>
</template>
<style scoped>
* {
	color: black;
}
</style>
