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
	if (!card) return;

	if (card.state === "Перевернуть") {
		setCardState(index, "Завершить");
		score.value += 1;
	} else {
		setCardState(index, "Перевернуть");
		score.value = Math.max(0, score.value - 1);
		setCardStatus(index, "pending");
	}
}

function setCardStatus(index, status) {
	data.value[index].status = status;
}

function setCardState(index, newState) {
	data.value[index].state = newState;
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
					:key="card.word"
					v-bind="card"
					:index="index"
					@turn-over-card="() => turnOverCard(index)"
					@set-status="(i, s) => setCardStatus(i, s)"
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
