<template>
  <div class="music-player">
    <transition :name="transitionName" mode="out-in">
      <img :key="currentTrack.cover" :src="currentTrack.cover" alt="Album cover" class="album-cover">
    </transition>
    <div class="controls">
      <button @click="prevTrack" :disabled="isFirstTrack">
        <i class="fas fa-backward"></i>
        <span>Prev</span>
      </button>
      <button @click="togglePlay">
        <i :class="isPlaying ? 'fas fa-pause' : 'fas fa-play'"></i>
        <span>{{ isPlaying ? 'Pause' : 'Play' }}</span>
      </button>
      <button @click="nextTrack" :disabled="isLastTrack">
        <i class="fas fa-forward"></i>
        <span>Next</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tracks: [
        { title: 'Track 1', cover: require('../assets/images/cover1.jpg') },
        { title: 'Track 2', cover: require('../assets/images/cover2.jpg') },
        { title: 'Track 3', cover: require('../assets/images/cover3.jpg') },
      ],
      currentIndex: 0,
      isPlaying: false,
      transitionName: 'slide-right',
    };
  },
  computed: {
    currentTrack() {
      return this.tracks[this.currentIndex];
    },
    isFirstTrack() {
      return this.currentIndex === 0;
    },
    isLastTrack() {
      return this.currentIndex === this.tracks.length - 1;
    },
  },
  methods: {
    prevTrack() {
      if (this.currentIndex > 0) {
        this.transitionName = 'slide-right';
        this.currentIndex--;
      }
    },
    nextTrack() {
      if (this.currentIndex < this.tracks.length - 1) {
        this.transitionName = 'slide-left';
        this.currentIndex++;
      }
    },
    togglePlay() {
      this.isPlaying = !this.isPlaying;
    },
  },
};
</script>

<style scoped>
.music-player {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  position: relative;
  overflow: hidden; /* Ensure that the transition is clipped to the container */
}

.album-cover {
  width: 100%;
  height: auto;
  border-radius: 10px;
}

.controls {
  display: flex;
  justify-content: space-around;
  width: 100%;
  margin-top: 20px;
}

button {
  background-color: transparent;
  border: none;
  color: #333333; /* Dark off-grey color */
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  align-items: center;
}

button:disabled {
  color: #cccccc; /* Lighter grey for disabled buttons */
  cursor: not-allowed;
}

button i {
  font-size: 20px;
}

button span {
  font-size: 12px;
  margin-top: 5px;
}

.slide-left-enter-active, .slide-left-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}

.slide-left-enter-from {
  opacity: 0;
  transform: translateX(100%);
}

.slide-left-leave-to {
  opacity: 0;
  transform: translateX(-100%);
}

.slide-right-enter-active, .slide-right-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}

.slide-right-enter-from {
  opacity: 0;
  transform: translateX(-100%);
}

.slide-right-leave-to {
  opacity: 0;
  transform: translateX(100%);
}
</style>