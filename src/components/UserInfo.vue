<script setup lang="ts">
import { defineProps, Ref } from 'vue';
import BaseBadge from './BaseBadge.vue';
interface Props {
	name: Ref<string>;
	description: Ref<string>;
	role: string;
}
const props = defineProps<Props>();
</script>
<template>
	<section>
		<div>
			<h3>{{ props.name }}</h3>
			<BaseBadge />
		</div>
		<p>{{ props.description }}</p>
	</section>
</template>

<style>
section {
	margin: 2rem auto;
	max-width: 30rem;
	border-radius: 12px;
	box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
	padding: 1rem;
}

section div {
	display: flex;
	justify-content: space-between;
	align-items: center;
}
</style>
