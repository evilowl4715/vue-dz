<script setup>
const props = defineProps({
	word: {
		type: String,
		required: true,
	},
	translation: {
		type: String,
		required: true,
	},
	state: {
		type: String,
		required: true,
		validator: (val) => ["Перевернуть", "Завершить"].includes(val),
	},
	status: {
		type: String,
		required: true,
		validator: (val) => ["pending", "success", "fail"].includes(val),
	},
	index: {
		type: Number,
		required: true,
	},
});
const emit = defineEmits(["turn-over-card", "set-status"]);

function turnOverCard() {
	emit("turn-over-card");
}

function yes() {
	emit("set-status", props.index, "success");
}

function no() {
	emit("set-status", props.index, "fail");
}
</script>
<template>
	<div class="card" :class="props.state === 'Завершить' ? 'reverted' : ''">
		<div v-show="props.state === 'Перевернуть'" class="card__block card-front">
			<div class="card__number">01</div>
			<div class="card__word">
				{{ props.word }}
			</div>
			<div class="card__bottom">
				<div class="card__action" @click="turnOverCard()">
					{{ props.state }}
				</div>
			</div>
		</div>

		<div v-show="props.state === 'Завершить'" class="card__block card-back">
			<div v-show="props.status === 'fail'">
				<svg
					width="48"
					height="48"
					viewBox="0 0 48 48"
					fill="none"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						fill-rule="evenodd"
						clip-rule="evenodd"
						d="M30.922 28.778L28.8 30.9L23.998 26.102L19.198 30.894L17.078 28.772L21.876 23.982L17.078 19.186L19.2 17.064L24 21.862L28.802 17.068L30.922 19.192L26.122 23.982L30.922 28.778ZM24 4.5C13.248 4.5 4.5 13.248 4.5 24C4.5 34.752 13.248 43.5 24 43.5C34.752 43.5 43.5 34.752 43.5 24C43.5 13.248 34.752 4.5 24 4.5Z"
						fill="#D00303"
					/>
				</svg>
			</div>
			<div v-show="props.status === 'success'">
				<svg
					width="36"
					height="36"
					viewBox="0 0 36 36"
					fill="none"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						fill-rule="evenodd"
						clip-rule="evenodd"
						d="M19.8129 24.1071L19.416 24.8105H17.8652L17.3982 24.1902C17.3705 24.1477 14.6252 20.0455 11.0769 17.8006L9.90462 17.0622L11.3852 14.7212L12.5538 15.4597C15.1108 17.0751 17.2338 19.4345 18.4855 21.0092C20.4517 18.0462 25.056 11.8745 32.1175 6.86954C28.8185 2.69354 23.7212 0 18 0C8.07508 0 0 8.07508 0 18C0 27.9249 8.07508 36 18 36C27.9249 36 36 27.9249 36 18C36 14.7932 35.1471 11.7877 33.672 9.17723C24.7495 15.5391 19.8665 24.0129 19.8129 24.1071Z"
						fill="#09BB00"
					/>
				</svg>
			</div>
			<div class="card__number">01</div>
			<div class="card__word">
				{{ props.translation }}
			</div>
			<div class="card__bottom">
				<div v-show="props.status == 'pending'" class="card__action">
					<button @click="no()">нет</button>
					<button @click="yes()">да</button>
				</div>
				<div
					v-show="props.status !== 'pending'"
					class="card__action"
					@click="turnOverCard()"
				>
					{{ props.state }}
				</div>
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
