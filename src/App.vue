<script setup lang="ts">
import { provide, ref, Ref } from 'vue';
import AddNewContact from './components/AddNewContact.vue';
import FriendContact from './components/FriendContact.vue';

type Contact = {
	id: string;
	name: string;
	phone: string;
	email: string;
	isFavourite: boolean;
};

const friendsList: Ref<Contact[]> = ref([
	{
		id: 'gosia',
		name: 'Małgorzata Boa',
		phone: `+48 999-999-999`,
		email: `gosia@localhost.com`,
		isFavourite: false,
	},
	{
		id: 'dominika',
		name: 'Dominika Boa',
		phone: `+48 111-111-111`,
		email: `dominika@localhost.com`,
		isFavourite: false,
	},
]);

provide('friendsListData', friendsList);

const toggleFavourite = (friendId: string) => {
	const identifyFriend = friendsList.value.find(friend => {
		return friend.id === friendId;
	});
	identifyFriend.isFavourite = !identifyFriend.isFavourite;
};

const addNewContact = (friendData: Contact) => {
	const createContactId = (friendData: Contact) => {
		const firstName = friendData.name.split(' ')[0];
		const firstLetterToLowerCase = firstName.slice(0, 1).toLowerCase();
		const restOfFirstName = firstName.slice(1);
		const idFromName = firstLetterToLowerCase + restOfFirstName;

		return idFromName;
	};

	friendData.id = createContactId(friendData);
	friendData.isFavourite = false;

	friendsList.value.push(friendData);
};
const deleteContact = (friendId: string) => {
	friendsList.value = friendsList.value.filter(
		friend => friend.id !== friendId
	);
};
const friendData = ref(undefined);
const passChoosenFriend = (friendId: string) => {
	let friendT = friendsList.value.find(friend => {
		return friend.id === friendId;
	});
	return (friendData.value = friendT);
};

provide('friendsListData', friendData);
</script>
<template>
	<header>
		<h1>FriendList</h1>
	</header>
	<section id="app">
		<AddNewContact @add-contact="addNewContact" />
		<FriendContact
			v-for="friend in friendsList"
			:friend="friend"
			@pass-choosen-friend="passChoosenFriend"
			@toggle-favourite="toggleFavourite"
			@delete-contact="deleteContact" />
	</section>
</template>
<style scoped></style>
