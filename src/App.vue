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
.app__title {
  text-align: center;
  margin-top: 2rem;
  margin-bottom: 1rem;
  font-size: 2.5rem;
}
</style>
