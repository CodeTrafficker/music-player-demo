<template>
  <div class="music-player">
    <transition :name="transitionName" mode="out-in">
      <img :key="currentTrack.cover" :src="currentTrack.cover" alt="Album cover" class="album-cover">
    </transition>
    <h3 class="track-title">{{ currentTrack.title }}</h3>
    <div class="controls">
      <div class="prev-next-buttons">
        <button @click="prevTrack">
          <i class="fas fa-backward"></i>
          <span>Prev</span>
        </button>
        <button @click="nextTrack">
          <i class="fas fa-forward"></i>
          <span>Next</span>
        </button>
      </div>
      <div class="play-button">
        <button @click="togglePlay">
          <i :class="isPlaying ? 'fas fa-pause' : 'fas fa-play'"></i>
          <span>{{ isPlaying ? 'Pause' : 'Play' }}</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tracks: [
        { title: 'John Cale - Antarctica Starts Here', cover: require('../assets/images/cover1.jpg') },
        { title: 'Harry Partch - Emergence Of The Spirit', cover: require('../assets/images/cover2.jpg') },
        { title: 'The Raincoats - Shouting Out Loud', cover: require('../assets/images/cover3.jpg') },
        { title: 'Massive Attack - Inertia Creeps', cover: require('../assets/images/cover4.jpg') },
        { title: 'Sleeping Tapes - See You At The Dreaming Tree', cover: require('../assets/images/cover5.jpg') },
        { title: 'Angelo Badalamenti - The Nightingale', cover: require('../assets/images/cover6.jpg') },
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
      this.transitionName = 'slide-right';
      if (this.currentIndex > 0) {
        this.currentIndex--;
      } else {
        this.currentIndex = this.tracks.length - 1; // Loop back to the last cover
      }
    },
    nextTrack() {
      this.transitionName = 'slide-left';
      if (this.currentIndex < this.tracks.length - 1) {
        this.currentIndex++;
      } else {
        this.currentIndex = 0; // Loop back to the first cover
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

.track-title {
  width: 100%;
  font-size: 1.2em; /* Reset to 1.2em */
  text-align: left;
  margin: 10px 0;
}

.controls {
  width: 100%;
}

.prev-next-buttons {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

.play-button {
  display: flex;
  justify-content: center;
  border-top: 1px solid #333333; /* 1px solid line on top */
  border-bottom: 1px solid #333333; /* 1px solid line on bottom */
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
  font-size: 24px; /* Increased to 24px */
}

button span {
  font-size: 15px; /* Reset to 15px */
  margin-top: 5px;
}

.slide-left-enter-active, .slide-left-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}

.slide-left-enter-from {
  opacity: 0;
  transform: translateX(100%);
}

.slide-left-enter-to {
  opacity: 1;
  transform: translateX(0);
}

.slide-left-leave-from {
  opacity: 1;
  transform: translateX(0);
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

.slide-right-enter-to {
  opacity: 1;
  transform: translateX(0);
}

.slide-right-leave-from {
  opacity: 1;
  transform: translateX(0);
}

.slide-right-leave-to {
  opacity: 0;
  transform: translateX(100%);
}
</style>