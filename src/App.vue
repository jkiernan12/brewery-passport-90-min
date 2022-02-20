<template>
  <img alt="Vue logo" class="beer-logo" src="./assets/beer-icon.svg">
  <MainPage msg="Brewery Passport"/>
</template>

<script>
import MainPage from './components/MainPage.vue'

export default {
  name: 'App',
  components: {
    MainPage
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.beer-logo {
  max-width: 300px;
}
</style>
