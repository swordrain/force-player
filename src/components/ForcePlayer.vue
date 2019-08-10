<template>
  <div class="force-player-container">
    <img v-if="initial" class="force-player-container-cover" :src="cover" />
    <div v-if="initial" class="force-player-playbtn" @click="startPlay">▷</div>
    <video ref="video" :height="height" :width="width">
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
    },
    cover: {
      type: String
    }
  },
  data: function() {
    return {
      initial: true
    };
  },
  methods: {
    startPlay: function() {
      this.initial = false;
      this.$refs.video.play();
    }
  }
};
</script>
<style scoped>
.force-player-container {
  position: relative;
  display: inline-block;
}
.force-player-container-cover {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 100;
}
.force-player-playbtn {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  color: white;
  font-size: 40px;
  border-radius: 50%;
  border: 1px solid white;
  width: 60px;
  height: 60px;
  text-align: center;
  line-height: 60px;
  z-index: 200;
}
.force-player-playbtn:hover {
  cursor: pointer;
  background: rgba(255, 255, 255, 0.5);
}
</style>