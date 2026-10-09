<template>
	<p v-bind:style="{
		backgroundColor: '#ccc',
		color: c
	}">El mensaje se ha enviado sastifactoriamente</p>
	<button @click="handleClick()">Cambiar color</button>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
	name: "ClaseBind",
	setup() {
		let c = ref('#ccc')
		const handleClick = () => {
			c.value = '#FD704D'
		}
		return {
			c, handleClick
		}
	},
	
})

</script>

<style>

</style>
