<script setup>
import { computed, ref, watch } from 'vue';

const enteredGoal = ref('');
const goals = ref([]);
const addGoal = () => {
	goals.value.push(enteredGoal.value);
	console.log(goals.value);
};
</script>
<template>
	<div>
		<header>
			<h1>Vue Course Goals</h1>
		</header>
		<section id="user-goals">
			<h2>My course goals</h2>
			<input type="text" v-model="enteredGoal" />
			<button @click="addGoal">Add Goal</button>
			<p v-if="goals.length === 0">
				No goals have been added yet - please start adding some!
			</p>
			<ul v-else>
				<li v-for="goal1 in goals">{{ goal1 }}</li>
			</ul>
		</section>
	</div>
</template>
<style scoped>
* {
	color: black;
}
</style>
