<script setup>
let date = new Date();
import { ref } from "vue";
import Button from "./components/Button.vue";
import Card from "./components/card.vue";
import Score from "./components/Score.vue";
let btnBg = "red";

const data = {
	wordFirst: "dust-coat",
	wordLast: "пыльник",
	actionFront: "ПЕРЕВЕРНУТЬ",
	actionBack: "ЗАВЕРШЕНО",
};

const reverted = ref(false);

const cards = ref(
	Array.from({ length: 5 }, () => ({
		reverted: false,
	}))
);

function turnOverCard() {
	reverted.value = !reverted.value;
}
</script>

<template>
	<header class="header">
		<div class="container">
			<div class="header__row">
				<div class="header__logo">ЗАПОМНИ СЛОВО</div>
				<Score count="5" />
			</div>
		</div>
	</header>
	<main>
		<div class="container">
			<div class="cards">
				<Card
					v-for="(card, index) in cards"
					:key="index"
					:class="reverted ? 'card reverted' : 'card'"
					:word="card.reverted ? data.wordLast : data.wordFirst"
					:action-front="data.actionFront"
					:action-back="data.actionBack"
					@turn-over-card="() => turnOverCard(index)"
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
