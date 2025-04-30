<script setup>
import HeaertIcon from "./icons/HeartIcon.vue";
defineProps({
	count: {
		type: Number,
		default: 0,
	},
});
</script>

<template>
	<div class="score">
		<span>{{ count }}</span>
		<HeaertIcon />
	</div>
</template>

<style scoped>
.score {
	box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.15);
	background: var(--border-color);
	display: flex;
	align-items: center;
	justify-self: center;
	border-radius: 36px;
	padding: 0 24px;
	height: 48px;
	box-sizing: border-box;
	gap: 10px;
	font-weight: 700;
	font-size: 16px;
	line-height: 150%;
	text-align: center;
	color: var(--color-blue);
}
</style>
