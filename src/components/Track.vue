<template>
  <div class="container" >
    <div class="background-track"></div>
  </div>
</template>
<script>
export default {
  props: {
    // disabled: {
    //   type: Boolean,
    //   default: false
    // }
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
  background-color: #E4E7ED;
}
</style>