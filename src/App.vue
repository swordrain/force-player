<template>
  <div id="app">
    <force-player cover="/cover.gif" width="640px" height="360px">
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
  color: #2c3e50;
  padding: 50px;
}
</style>
