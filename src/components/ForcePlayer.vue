<template>
  <div class="force-player-container" @mouseenter="toggleToolbox" @mouseleave="toggleToolbox">
    <img v-if="initial" class="force-player-container-cover" :src="cover" />
    <div v-if="initial" class="force-player-playbtn" @click="startPlay">▷</div>
    <video ref="video" :height="height" :width="width">
      <slot></slot>
    </video>
    <transition name="slide-down-fade">
      <div v-show="showToolbox" class="force-player-title">{{title}}</div>
    </transition>
    <transition name="slide-up-fade">
      <div v-show="showToolbox" class="force-player-toolbox">
        <button class="force-player-play-btn" @click="changePlayState">{{ playing ?'▢':'▷'}}</button>
        <span
          class="force-player-progress-display"
        >{{displayTime(currentTime)}} / {{displayTime(duration)}}</span>
        <div style="flex:1;margin: 0 10px;transform: translateY(-3px);">
          <Track
            :progress="progress"
            @progressChanging="changeCurrentTime"
            @progressChanged="changeCurrentTime"
          />
        </div>
        <div style="width:100px;transform: translateY(-3px);margin-right: 10px;">
          <Track
            :progress="volume"
            @progressChanging="changeVolumn"
            @progressChanged="changeVolumn"
          />
        </div>
        <button class="force-player-fullscreen-btn" @click="fullscreen">FS</button>
      </div>
    </transition>
  </div>
</template>
<script>
import Track from "./Track";
export default {
  components: {
    Track
  },
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
    },
    title: {
      type: String
    }
  },
  data: function() {
    return {
      initial: true,
      showToolbox: false,
      volume: 100,
      progress: 0,
      playing: false,
      duration: 0,
      currentTime: 0
    };
  },
  methods: {
    startPlay() {
      this.initial = false;
      this.$refs.video.play();
    },
    changePlayState() {
      if (this.playing) {
        this.$refs.video.pause();
      } else {
        this.$refs.video.play();
      }
    },
    toggleToolbox() {
      if (!this.initial) {
        this.showToolbox = !this.showToolbox;
      }
    },
    changeVolumn(volume) {
      this.volume = volume;
    },
    fullscreen() {
      this.$refs.video.requestFullscreen();
    },
    displayTime(time) {
      const minute = parseInt(time / 60);
      const second = parseInt(time % 60);
      return (
        (minute < 10 ? "0" + minute : minute) +
        ":" +
        (second < 10 ? "0" + second : second)
      );
    },
    changeCurrentTime(progress) {
      this.progress = progress;
      this.currentTime = (progress / 100) * this.duration;
      this.$refs.video.currentTime = this.currentTime;
    }
  },
  watch: {
    volume: function() {
      this.$refs.video.volume = this.volume / 100;
    }
  },
  mounted: function() {
    this.$refs.video.addEventListener("durationchange", e => {
      this.duration = e.target.duration;
    });
    this.$refs.video.addEventListener("timeupdate", e => {
      this.currentTime = e.target.currentTime;
      this.progress = (e.target.currentTime / this.duration) * 100;
    });
    this.$refs.video.addEventListener("playing", e => {
      this.playing = true;
    });
    this.$refs.video.addEventListener("pause", e => {
      this.playing = false;
    });
    this.$refs.video.addEventListener("ended", e => {
      this.playing = false;
    });
  }
};
</script>
<style scoped>
.force-player-container {
  position: relative;
  display: inline-block;
  overflow: hidden;
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
.force-player-toolbox {
  background: rgba(255, 255, 255, 0.5);
  position: absolute;
  height: 30px;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  padding: 10px;
  align-items: center;
}
.force-player-title {
  background: rgba(255, 255, 255, 0.5);
  position: absolute;
  height: 30px;
  top: 0;
  left: 0;
  right: 0;
  line-height: 30px;
  text-align: center;
}
.slide-down-fade-enter-active {
  transition: all 0.3s linear;
}
.slide-down-fade-leave-active {
  transition: all 0.3s linear;
}
.slide-down-fade-enter,
.slide-down-fade-leave-to {
  transform: translateY(-100%);
  opacity: 0;
}
.slide-up-fade-enter-active {
  transition: all 0.3s linear;
}
.slide-up-fade-leave-active {
  transition: all 0.3s linear;
}
.slide-up-fade-enter,
.slide-up-fade-leave-to {
  transform: translateY(100%);
  opacity: 0;
}
.force-player-play-btn {
  background: none;
  outline: none;
  border: none;
  box-sizing: border-box;
  width: 24px;
  font-size: 20px;
}
.force-player-play-btn:hover {
  cursor: pointer;
  color: #409eff;
}
.force-player-fullscreen-btn {
  background: none;
  outline: none;
  border: none;
  box-sizing: border-box;
  width: 20px;
  font-size: 12px;
  border-radius: 3px;
  border: 1px solid #409eff;
  padding: 0;
}
.force-player-fullscreen-btn:hover {
  cursor: pointer;
  color: #409eff;
}
.force-player-progress-display {
  font-size: 14px;
}
</style>