<script setup lang="ts">
import { defineEmits, defineProps, ref, Ref, computed } from 'vue';
import ContactData from './ContactData.vue';
import PersonData from './PersonData.vue';
interface Props {
	friend: Contact;
}
interface Emit {
	(eventName: 'toggleFavourite', friendId: string): void;
	(eventName: 'deleteContact', friendId: string): void;
	(eventName: 'passChoosenFriend', friendId: string): void;
}
type Contact = {
	id: string;
	name: string;
	phone: string;
	email: string;
	isFavourite: boolean;
};
const emit = defineEmits<Emit>();
const props = defineProps<Props>();
const detailsAreVisible: Ref<boolean> = ref(false);
const isContactDataShown: Ref<boolean> = ref(false);
const isPersonDataShown: Ref<boolean> = ref(false);

const showDetails = (value: string, friendId: string) => {
	if (value === 'showDetails') {
		detailsAreVisible.value = !detailsAreVisible.value;
	} else if (value === 'showContactData') {
		isContactDataShown.value = !isContactDataShown.value;
		isPersonDataShown.value = false;
	} else if (value === 'showPersonData') {
		isPersonDataShown.value = !isPersonDataShown.value;
		isContactDataShown.value = false;
	}
	if (friendId !== undefined) {
		emit('passChoosenFriend', friendId);
	}
};
const printShowOrHide = computed(value => {
	return value ? 'Show' : 'Hide';
});
</script>
<template>
	<ul>
		<li>
			<h2>{{ friend.name }}{{ friend.isFavourite ? '(Favourite)' : '' }}</h2>
			<button @click="showDetails('showDetails', undefined)">
				{{ detailsAreVisible ? 'Hide' : 'Show' }} details
			</button>
			<button @click="$emit('toggleFavourite', friend.id)">
				Add to favourite
			</button>
			<ul v-if="detailsAreVisible">
				<ContactData v-if="isContactDataShown" />
				<PersonData v-if="isPersonDataShown" />
				<button @click="showDetails('showContactData', friend.id)">
					Show contact data
				</button>
				<button @click="showDetails('showPersonData', friend.id)">
					Show friend data
				</button>
			</ul>
		</li>
		<button @click="$emit('deleteContact', friend.id)">Delete</button>
	</ul>
</template>
<style scoped></style>
