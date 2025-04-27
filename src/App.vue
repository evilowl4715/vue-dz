<script setup>
let date = new Date();
import Button from './components/Button.vue';
let btnBg = "red";
</script>

<template>
	<header></header>
	<main>{{ date }}</main>
	<footer>
		<Button :customClass="`${btnBg}`">Button</Button>
	</footer>
</template>

<style scoped>
.red {
	background: red;
}
</style>
