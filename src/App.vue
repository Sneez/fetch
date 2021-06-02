<template>
  <div id="app">
    <Fetch />
  </div>
</template>

<script>
import Fetch from './components/Fetch.vue'

export default {
  name: 'App',
  components: {
    Fetch
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
