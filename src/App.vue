<template>
  <Contact />
</template>

<script>
import Contact from './components/Contact.vue'

export default {
  name: 'App',
  components: {
    Contact
  }
}
</script>

<style>
body {
  background-color: #333;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
