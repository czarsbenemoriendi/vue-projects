<script setup>
import { computed, ref, watch } from 'vue';

let counter = ref();
let result = ref(0);
// const w = watch(result, () => {
// 	if (result.value > 5) {
// 		setTimeout(() => {
// 			result.value = 0;
// 		}, 2000);
// 	}
// });
const inc = value => {
	return (result.value += value);
};
const decr = value => {
	return (result.value -= value);
};
const w2 = computed(() => {
	if (result.value < 37) {
		return 'Not there yet';
	} else if (result.value === 37) {
		return 'Enough!';
	} else {
		return 'Too much!';
	}
});
watch(result, () => {
	setTimeout(() => {
		result.value = 0;
	}, 3000);
});
</script>
<template>
	<div>
		<button @click="inc(5)">Add 5</button>
		<button @click="inc(1)">Add 1</button>
		<!-- 1) Connect the buttons and calculate a value (a number) -->
		<!-- Show "Not there yet" until you reach a result of exactly 37 -->
		<!-- Show "Too much!" if the result is greater than 37 -->
		<p>{{ w2 }}: {{ result }}</p>
		<!-- 2) Watch for changes in "result" and reset the value to 0 after 5 seconds -->
	</div>
</template>
<style scoped>
* {
	color: black;
}
</style>
