<template>
	<h1 v-if="age < 18">Es menor de edad</h1>
	<h1 v-else>Es mayor de edad</h1>
</template>

<script lang="ts" setup>
 	let age = 11;
</script>

<style scoped>
	
</style>