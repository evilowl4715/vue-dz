<script setup></script>

<template>
	<button class="btn"><slot /></button>
</template>

<style scoped>
.btn {
	background: var(--color-blue);
	color: var(--color-white);
	display: flex;
	justify-content: center;
	align-items: center;
	border-radius: 100px;
	max-width: 335px;
	width: 100%;
	height: 68px;
	transition: all 0.3s ease;
	border: none;
	cursor: pointer;
	font-family: var(--font);
	font-weight: 400;
	font-size: 24px;
	line-height: 150%;
	text-align: center;
}

.btn:hover {
	background: var(--color-blue-hover);
}
</style>
