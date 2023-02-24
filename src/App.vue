<template>
  <HelloWorldTest msg="AZTRO"/>
</template>

<script>
import HelloWorldTest from './components/HelloWorldTest.vue'

export default {
  name: 'App',
  components: {
    HelloWorldTest
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
