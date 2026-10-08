<template>
  <ul>
  	<span>Paises</span>
    <li v-for="country in countries" v-bind:key="country">
      {{ country }}
    </li>
  </ul>
</template>

<script lang="ts" setup>
import { ref } from 'vue';


const countries = ref(['Spain', 'France', 'UK', 'Italy', 'Portugal']);
</script>

<style scoped></style>