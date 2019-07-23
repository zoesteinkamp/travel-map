<template>
  <div id="app">
    <TheNavBar/>
    <MainPage/>
  </div>
</template>

<script>
import MainPage from './components/MainPage.vue'
import TheNavBar from './components/TheNavBar.vue'
import TheFooter from './components/TheFooter.vue'


export default {
  name: 'app',
  components: {
    TheNavBar,
    MainPage,
    TheFooter
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
