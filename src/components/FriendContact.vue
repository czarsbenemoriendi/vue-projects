<script setup lang="ts">
import { defineEmits, defineProps, ref, Ref, toRefs } from 'vue';
interface Props {
	friendList: Contact[];
	detailsAreVisible: boolean;
}
interface Emit {
	(eventName: 'showDetails'): void;
}
type Contact = {
	id: string;
	name: string;
	phone: string;
	email: string;
};
const emit = defineEmits<Emit>();
const props = defineProps<Props>();
</script>
<template>
	<ul>
		<li v-for="friend in friendList" :key="friend.id">
			<h2>{{ friend.name }}</h2>
			<button @click="$emit('showDetails', friend.id)">
				{{ props.detailsAreVisible ? 'Hide' : 'Show' }} details
			</button>
			<ul v-if="detailsAreVisible">
				<li><strong>Phone:</strong> {{ friend.phone }}</li>
				<li><strong>Email:</strong> {{ friend.email }}</li>
			</ul>
		</li>
	</ul>
</template>
<style scoped></style>
