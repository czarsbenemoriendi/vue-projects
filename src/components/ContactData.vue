<script setup lang="ts">
import { inject, InjectionKey, Ref } from 'vue';
type Contact = {
	id: string;
	name: string;
	phone: string;
	email: string;
	isFavourite: boolean;
};

const friendsListData: InjectionKey<Ref<Contact[]>> = inject('friendsListData');
let friendData = friendsListData.value;

console.log(friendData);
// console.log(friendsListData.value.phone);
// const newFriendData = friendData.map((friend, friendId) =>
// 	friendData.find(friend => {
// 		return friend.id === friend;
// 	})
// );
</script>

<template>
	<li><strong>Phone:</strong> {{ friendData.phone }}</li>
	<li><strong>Email:</strong> {{ friendData.email }}</li>
</template>
<style scoped></style>
