<script setup>
import ZipCodeFinder from './components/ZipCodeFinder.vue';

</script>

<template>
  <div class="app">
    <h1 class="app__title">Zip-code finder</h1>
    <zip-code-finder></zip-code-finder>

    <div class="app_subtitle">@made by <a class="app__link" href="https://github.com/GabrielMaksimovich">Baturinskyi Maksym</a>, see my <a class="app__link" href="https://my-portfolio-gb.netlify.app/">other projects</a></div>
  </div>
</template>

<style scoped>
.app {
  align-items: center;
  background: linear-gradient(#121212,#212b46);
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: center;
}


.app__title {
  animation: flipTitle 2s;
  color: #fff;
  font-size: 85px;
}

.app_subtitle {
  color: white;
}

.app__link {
  text-decoration: underline;
}

</style>
