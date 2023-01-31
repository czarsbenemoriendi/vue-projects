<script setup>
import { computed, ref, watch } from 'vue';

let playerHealth = ref(100);
let monsterHealth = ref(100);
let attackValue;
let currentRound = ref(0);
let winner = null;

const getRandomVal = (min, max) => {
	return Math.floor(Math.random() * (max - min)) + min;
};

const mayUseSpecialAttack = computed(() => {
	return currentRound.value % 3 !== 0;
});
const monsterBarStyles = computed(() => {
	if (monsterHealth.value < 0) return { width: '0%' };
	return { width: monsterHealth.value + '%' };
});
const playerBarStyles = computed(() => {
	if (playerHealth.value < 0) return { width: '0%' };
	return { width: playerHealth.value + '%' };
});

watch(playerHealth, value => {
	if (value <= 0 && monsterHealth <= 0) {
		winner = 'draw';
	} else if (value <= 0) {
		winner = 'monster';
	}
});
watch(monsterHealth, value => {
	if (value <= 0 && playerHealth <= 0) {
		winner = 'draw';
	} else if (value <= 0) {
		winner = 'player';
	}
});

const startGame = () => {
	monsterHealth.value = 100;
	playerHealth.value = 100;
	winner = null;
	currentRound.value = 0;
};
const monsterAttack = () => {
	currentRound.value++;
	attackValue = getRandomVal(5, 12);
	monsterHealth.value -= attackValue;
	setTimeout(playerAttack, 500);
};
const playerAttack = () => {
	attackValue = getRandomVal(8, 12);
	playerHealth.value -= attackValue;
};
const specialAttackMonster = () => {
	currentRound.value++;
	attackValue = getRandomVal(10, 25);
	monsterHealth.value -= attackValue;
	setTimeout(specialAttackPlayer, 500);
};
const specialAttackPlayer = () => {
	attackValue = getRandomVal(10, 25);
	playerHealth.value -= attackValue;
};
const healPlayer = () => {
	currentRound.value++;
	const healValue = getRandomVal(8, 20);
	if (playerHealth.value + healValue > 100) {
		playerHealth.value = 100;
	} else {
		playerHealth.value += healValue;
	}
	setTimeout(specialAttackPlayer, 500);
};
const surrender = () => {
	winner = 'monster';
};
</script>
<template>
	<div>
		<header>
			<h1>Monster Slayer</h1>
		</header>
		<div id="game">
			<section id="monster" class="container">
				<h2>Monster Health</h2>
				<div class="healthbar">
					<div class="healthbar__value" :style="monsterBarStyles"></div>
				</div>
			</section>
			<section id="player" class="container">
				<h2>Your Health</h2>
				<div class="healthbar">
					<div class="healthbar__value" :style="playerBarStyles"></div>
				</div>
			</section>
			<div class="container" v-if="winner">
				<h2>Game over!</h2>
				<h3 v-if="winner === 'player'">You win</h3>
				<h3 v-else-if="winner === 'monster'">You lost!</h3>
				<h3 v-else>It's a draw!</h3>
				<button @click="startGame">Start new game</button>
			</div>
			<section id="controls">
				<button @click="monsterAttack">ATTACK</button>
				<button @click="specialAttackMonster" :disabled="mayUseSpecialAttack">
					SPECIAL ATTACK
				</button>
				<button @click="healPlayer">HEAL</button>
				<button @click="surrender">SURRENDER</button>
			</section>
			<section id="log" class="container">
				<h2>Battle Log</h2>
				<ul></ul>
			</section>
		</div>
	</div>
</template>
<style scoped>
* {
	color: black;
}
</style>
