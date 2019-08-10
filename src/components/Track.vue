<template>
  <div class="container">
    <div class="background-track"></div>
    <div class="progress" :style="{width:progress+'%'}"></div>
    <div class="handler" :style="{left:progress+'%'}"></div>
  </div>
</template>
<script>
export default {
  props: {
    progress: {
      type: Number,
      default: 50,
      validator: function(value) {
        return value >= 0 && value <= 100;
      }
    }
  }
};
</script>
<style scoped>
.container {
  position: relative;
}
.background-track {
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  height: 5px;
  border-radius: 3px;
  background-color: #e4e7ed;
  z-index: 1000;
}
.progress {
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  height: 5px;
  border-radius: 3px;
  background-color: #409eff;
  z-index: 2000;
}
.handler {
  position: absolute;
  height: 8px;
  width: 8px;
  border: 2px solid #409eff;
  border-radius: 50%;
  background-color: white;
  z-index: 3000;
  transform: translate(-50%, -4px); /* 调整一下居中 */
}
.handler:hover {
  cursor: pointer;
}
</style>