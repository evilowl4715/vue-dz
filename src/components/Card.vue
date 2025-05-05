<script setup>
const { word, actionFront, actionBack } = defineProps({
	word: {
		type: String,
		default: "нету слова",
	},
	actionFront: {
		type: String,
		default: "ПЕРЕВЕРНУТЬ",
	},
	actionBack: {
		type: String,
		default: "ЗАВЕРШИТЬ",
	},
	reverted: { type: Boolean, default: false },
});

const emit = defineEmits({
	turnOverCard(payload) {
		return payload;
	},
});

function turnOverCard() {
	emit("turnOverCard", {
		word: word,
		actionFront: actionFront,
		actionBack: actionBack,
	});
}
</script>

<template>
	<div class="card" :class="{ reverted: reverted }">
		<div class="card__block card-front">
			<div class="card__number">01</div>
			<div class="card__word">
				{{ word }}
			</div>
			<div class="card__bottom">
				<div class="card__action" @click="turnOverCard()">
					{{ actionFront }}
				</div>
			</div>
		</div>

		<div class="card__block card-back">
			<div class="card__number">01</div>
			<div class="card__word">
				{{ word }}
			</div>
			<div class="card__bottom">
				<div class="card__action" @click="turnOverCard()">{{ actionBack }}</div>
			</div>
		</div>
	</div>
</template>

<style scoped>
.card {
	box-shadow: 0 0 16px 0 rgba(0, 0, 0, 0.1);
	background: var(--color-white);
	border-radius: 16px;
	box-sizing: border-box;
	background: #fff;
	position: relative;
	height: 376px;
	transform-style: preserve-3d;
	transition: transform 0.6s ease-in-out;
}

.card:hover {
	box-shadow: 10px 10px 10px 0 rgba(0, 0, 0, 0.05);
}

.card__block {
	border: 1px solid #cce8ff;
	border-radius: 12px;
	display: flex;
	align-items: center;
	justify-self: center;
	box-sizing: border-box;
	padding: 30px 20px;
	width: 100%;
	left: 50%;
	top: 50%;
	transform: translate(-50%, -50%);
	position: absolute;
	width: calc(100% - 38px);
	height: calc(100% - 56px);
	backface-visibility: hidden;
}

.card-front {
	z-index: 2;
}

.card-back {
	transform: translate(-50%, -50%) rotateY(180deg);
	z-index: 1;
}

.card__number {
	font-weight: 400;
	font-size: 14px;
	text-align: center;
	color: #000;
	position: absolute;
	top: -7px;
	left: 16px;
	width: 16px;
	height: 16px;
	background: #fff;
	display: flex;
	align-items: center;
	justify-self: center;
}

.card__word {
	font-weight: 400;
	font-size: 18px;
	text-align: center;
	color: #000;
	width: 100%;
}

.card__bottom {
	position: absolute;
	bottom: -7px;
	left: 50%;
	transform: translateX(-50%);
}

.card__action {
	padding: 0px 4px;
	height: 18px;
	box-sizing: border-box;
	background: #fff;
	cursor: pointer;
}

.card {
	width: calc(25% - 81px);
	perspective: 1000px;
}

.card.reverted {
	transform: rotateY(180deg);
}
</style>
