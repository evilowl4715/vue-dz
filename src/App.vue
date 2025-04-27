<script setup>
let date = new Date();
import Button from './components/Button.vue';
</script>

<template>
	<header></header>
	<main>{{ date }}</main>
	<footer>
		<Button>Button</Button>
	</footer>
</template>

<style scoped></style>
