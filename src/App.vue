<script setup>
let date = new Date();
import { computed, ref } from "vue";
import Button from "./components/Button.vue";
import Card from "./components/card.vue";
import Score from "./components/Score.vue";
let btnBg = "red";

const score = ref(0);

const data = ref([
	{
		word: "dust-coat",
		translation: "пыльник",
		state: "Перевернуть",
		status: "pending",
	},
	{
		word: "unadmitted",
		translation: "непризнанный",
		state: "Завершить",
		status: "fail",
	},
	{
		word: "armour-piercer",
		translation: "бронебойный",
		state: "Завершить",
		status: "success",
	},
	{
		word: "stamen",
		translation: "тычинка",
		state: "Перевернуть",
		status: "pending",
	},
]);

function turnOverCard(index) {
	const card = data.value[index];
	if (card.state === "Перевернуть") {
		card.state = "Завершить";
		score.value += 1;
	} else if (card.state === "Завершить") {
		card.state = "Перевернуть";
		score.value -= 1;
		card.status = "pending";
	}
}

function setStatus(index, newStatus) {
	data.value[index].status = newStatus;
}
</script>

<template>
	<header class="header">
		<div class="container">
			<div class="header__row">
				<div class="header__logo">ЗАПОМНИ СЛОВО</div>
				<Score :count="score" />
			</div>
		</div>
	</header>
	<main>
		<div class="container">
			<div class="cards">
				<Card
					v-for="(card, index) in data"
					v-bind="card"
					:key="card.word"
					@turn-over-card="() => turnOverCard(index)"
					@setStatus="(newStatus) => setStatus(index, newStatus)"
				/>
			</div>
		</div>
		{{ date }}
	</main>
	<footer>
		<Button :customClass="`${btnBg}`">Button</Button>
	</footer>
</template>

<style scoped>
.header {
	height: 121px;
	display: flex;
	align-items: center;
}

.header__row {
	display: flex;
	justify-content: space-between;
	align-items: center;
}

.cards {
	display: flex;
	flex-wrap: wrap;
	gap: 107px;
}
</style>
