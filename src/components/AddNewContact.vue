<script setup lang="ts">
import { ref, Ref, defineEmits, defineProps } from 'vue';

interface Emit {
	(eventName: 'add-contact', friendData: FriendData): void;
}
type FriendData = {
	name: string;
	phone: string;
	email: string;
};

const emit = defineEmits<Emit>();
const friendName = ref('');
const friendPhone = ref('');
const friendMail = ref('');

// how to type these parametrs
const storeDataAboutNewContact = (
	dataName: string,
	dataPhone: string,
	dataMail: string
) => {
	const friendData: FriendData = {
		name: dataName,
		phone: dataPhone,
		email: dataMail,
	};
	emit('add-contact', friendData);
};
</script>
<template>
	<form @submit.prevent>
		<h2>Add new contact</h2>
		<div>
			<label>Name</label>
			<input type="text" v-model="friendName" />
		</div>
		<div>
			<label>Phone</label>
			<input type="text" v-model="friendPhone" />
		</div>
		<div>
			<label>E-mail</label>
			<input type="text" v-model="friendMail" />
		</div>
		<div>
			<button
				type="submit"
				@click="storeDataAboutNewContact(friendName, friendPhone, friendMail)">
				Submit
			</button>
		</div>
	</form>
</template>
<style scoped>
form {
	display: flex;
	flex-direction: column;
	align-items: center;
	border: 1px solid gray;
	width: 80%;
	margin: 0 auto;
}
div {
	display: flex;
	flex-direction: column;
	align-items: center;
	font-size: 2rem;
}
input {
	border: 1px solid gray;
	border-radius: 10px;
	text-align: center;
	margin: 0.5em auto;
	padding: 1px;
	font-size: 2rem;
}

button {
	margin-bottom: 1rem;
}
</style>
