<template>
  <div id="app">
    <Track :progress="30"/>
  </div>
</template>

<script>
import Track from './components/Track'
export default {
  name: 'app',
  components: {
    Track
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
  padding: 50px;
}
</style>
