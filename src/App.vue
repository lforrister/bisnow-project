<template>
  <div id="app" class="min-h-screen bg-gradient-to-br from-blue-200 flex justify-center flex-col p-5">
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
}
</style>
