<script setup>
import ZipCodeFinder from './components/ZipCodeFinder.vue';

</script>

<template>
  <div class="app">
    <h1 class="app__title">Zip Code Finder</h1>
    <zip-code-finder></zip-code-finder>
  </div>
</template>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;

  background: aqua;
  max-width: 500px;
  margin: 15rem auto;
  padding: 1.5rem;
  border-radius: 1rem;
}
.app__title {
  text-align: center;
  font-size: 2.5rem;
}
</style>
