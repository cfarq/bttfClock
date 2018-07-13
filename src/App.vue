<template>
  <div id="app">

    <Clock countdown-date="2018-10-24 08:15:00"></Clock>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Clock from './components/clock'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Clock
  }
}
</script>

<style>
  body {
    background-color: black;
  }

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: black;
  margin-top: 60px;
}


</style>
