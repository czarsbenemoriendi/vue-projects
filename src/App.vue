<script setup>
import { ref } from 'vue';
const counter = ref(0);
const inc = n => {
	counter.value += n;
};
const red = n => {
	counter.value -= n;
};
const name = ref('');
const confirmName = ref('');
const confirmedName = () => {
	confirmName.value = name.value;
};
const setName = e => {
	name = e.target.value;
};
</script>
<template>
	<div>
		<header>
			<h1>Vue Events</h1>
		</header>
		<section id="events">
			<h2>Events in Action</h2>
			<button @click="inc(10)">Add</button>
			<button @click="red(5)">Remove</button>
			<p>Result: {{ counter }}</p>
			<input type="text" v-model="name" @keyup.enter="confirmedName" />
			<p>Your name: {{ confirmName }}</p>
		</section>
	</div>
</template>
<style scoped>
* {
	color: black;
}
</style>
