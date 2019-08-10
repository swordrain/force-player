<template>
  <div
    ref="track"
    class="track-container"
    :style="{'point-event':disabled?'none':'inherit'}"
    @click="jumpProgress"
  >
    <div class="background-track"></div>
    <div class="progress" :style="{width:innerProgress+'%'}"></div>
    <div class="handler" :style="{left:innerProgress+'%'}" @mousedown="startDragging"></div>
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
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },

  data: function() {
    return {
      innerProgress: this.progress,
      isDragging: false,
      draggingOriginPoint: 0
    };
  },
  methods: {
    startDragging: function(e) {
      if (!this.disabled) {
        this.$emit("startDragging");
        this.isDragging = true;
        this.draggingOriginPoint = e.clientX;
        this.draggingOriginProgress = this.innerProgress;
        document.addEventListener("mousemove", this.dragging);
        document.addEventListener("mouseup", this.endDragging);
      }
    },
    dragging: function(e) {
      if (this.isDragging) {
        const width = getComputedStyle(this.$refs.track).width;
        this.innerProgress =
          this.draggingOriginProgress +
          ((e.clientX - this.draggingOriginPoint) / parseInt(width)) * 100;
        this.$emit("progressChanged", this.innerProgress);
      }
    },
    endDragging: function() {
      if (this.isDragging) {
        this.$emit("endDragging");
        this.isDragging = false;
        document.removeEventListener("mousemove", this.dragging);
        document.removeEventListener("mouseup", this.endDragging);
      }
    },
    jumpProgress: function(e) {
      this.innerProgress =
        (e.offsetX / parseInt(getComputedStyle(this.$refs.track).width)) * 100;
      this.$emit("progressChanged", this.innerProgress);
    }
  }
};
</script>
<style scoped>
.track-container {
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
  transform: translate(-50%, -4px); /*  居中 */
}
.container:hover {
  cursor: pointer;
}
</style>