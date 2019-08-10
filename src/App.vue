<template>
  <div id="app">
    <force-player>
      <source src="/sample.mp4" type="video/mp4" />
    </force-player>
  </div>
</template>

<script>
import ForcePlayer from "./components/ForcePlayer";
export default {
  name: "app",
  components: {
    ForcePlayer
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 50px;
}
</style>
