<template>
  <div id="app">
    <MusicPlayer />
  </div>
</template>

<script>
import MusicPlayer from './components/MusicPlayer.vue';

export default {
  name: 'App',
  components: {
    MusicPlayer,
  },
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
  background-color: #f0f0f0;
}

#app {
  width: 300px;
  background-color: #fff;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  overflow: hidden;
}
</style>