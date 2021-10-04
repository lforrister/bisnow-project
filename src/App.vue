<template>
  <div id="app">
    <EmailDirectory />
  </div>
</template>

<script>
import EmailDirectory from './components/EmailDirectory.vue'

export default {
  name: 'App',
  components: {
    EmailDirectory,
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
