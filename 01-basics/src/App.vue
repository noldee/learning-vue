<template>
  <h1>Listado de posts: </h1>
  <PostContainer />
 <CounterOption />
 <CounterOption />
 <CounterOption />
  <CounterComposition />
</template>


<script lang="ts" setup>
 
   import PostContainer from './components/PostContainer.vue';
   import CounterOption from './components/CounterOption.vue';
   import CounterComposition from './components/CounterComposition.vue';
</script>

<style scoped>

  h1{
    color: green;
  }

</style>
