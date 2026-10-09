<template>
  <ul>
  	<span>Paises</span>
    <li v-for="country in countries" v-bind:key="country.code">
      {{ country.name }}
    </li>
  </ul>
</template>

<script lang="ts" setup>
import { ref, type Ref } from 'vue';

interface Country {
  code: string,
  name: string
}

const countries: Ref<Array<Country>> = ref([
  {
    code: "es",
    name: "Spain"
  },
  {
    code: "en",
    name: "UK"
  },
  {
    code: "fr",
    name: "france"
  },
  {
    code: "it",
    name: "Italy"
  }
]);
</script>

<style scoped></style>
