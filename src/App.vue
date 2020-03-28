<template>
  <div id="app">
    <img alt="Matkalasku logo" src="./assets/logo2.png">
    <Matkalasku msg="Matkalasku sovellus"/>
  </div>
</template>

<script>
import Matkalasku from './components/Matkalasku.vue'

export default {
  name: 'App',
  components: {
    Matkalasku
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
</style>
