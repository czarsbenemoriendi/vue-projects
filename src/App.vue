<script setup lang="ts">
import { ref, Ref } from 'vue';
import FriendContact from './components/FriendContact.vue';

type Contact = {
	id: string;
	name: string;
	phone: string;
	email: string;
};
const detailsAreVisible: Ref<boolean> = ref(false);
const friendList: Ref<Contact[]> = ref([
	{
		id: 'gosia',
		name: 'Małgorzata Zimnicka',
		phone: `+48 999-999-999`,
		email: `gosia@localhost.com`,
	},
	{
		id: 'dominika',
		name: 'Dominika Kędzierska',
		phone: `+48 999-999-999`,
		email: `dominika@localhost.com`,
	},
]);

const showDetails = (id: string) => {
	console.log(id);
	detailsAreVisible.value = !detailsAreVisible.value;
};
</script>
<template>
	<header>
		<h1>FriendList</h1>
	</header>
	<section id="app">
		<FriendContact
			:friendList="friendList"
			:detailsAreVisible="detailsAreVisible"
			@show-details="showDetails" />
	</section>
</template>
<style scoped></style>
