<script setup lang="ts">
import { ref } from 'vue';
import UserInfo from './components/UserInfo.vue';
import BadgeList from './components/BadgeList.vue';
import TheHeader from './components/TheHeader.vue';

const name = ref('Maximilian Schwarzmüller');
const description = ref('Site owner and admin');
const role = ref('admin');
</script>

<template>
	<div>
		<TheHeader />
		<BadgeList />
		<UserInfo :fullName="name" :infoText="description" :role="role" />
	</div>
</template>

<style>
html {
	font-family: sans-serif;
}

body {
	margin: 0;
}
</style>
