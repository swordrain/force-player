<template>
  <div class="force-player-container">
    <video :height="height" :width="width">
      <slot></slot>
    </video>
  </div>
</template>
<script>
export default {
  props: {
    width: {
      type: String,
      default: "600px"
    },
    height: {
      type: String,
      default: "400px"
    }
  }
};
</script>
<style scoped>
</style>