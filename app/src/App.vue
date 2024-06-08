<template>
  <div class="app__header">
    <h1>How fast is your reflex</h1>
    <button
      @click="start"
      :disabled="isPlaying"
      :class="isPlaying ? 'un-touchable' : ''"
    >
      {{ playButtonText }}
    </button>
  </div>
  <RandomBlock
    v-if="isPlaying"
    :delay="delay"
    @end="endGame"
  />
  <Result
    v-if="showResults"
    :score="score"
  />
</template>

<script setup>
  import { ref } from 'vue';
  import RandomBlock from './components/RandomBlock.vue';
  import Result from './components/Result.vue';

  const isPlaying = ref(false);
  const delay = ref(null);
  const score = ref(null);
  const showResults = ref(false);
  const playButtonText = ref('Play');

  function start() {
    delay.value = 2000 + Math.random() * 5000;
    isPlaying.value = true;
    showResults.value = false;
    playButtonText.value = 'Steady ....';
  }

  function endGame(reactionTime) {
    score.value = reactionTime;
    isPlaying.value = false;
    showResults.value = true;
    playButtonText.value = 'Play again';
  }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    width: 100vw;
    height: 100vh;
  }
  .app__header {
    padding: 1rem;
    height: 10rem;
  }
  .app__header h1 {
    margin: 0rem;
  }
  .un-touchable {
    pointer-events: none;
  }
  button {
    margin-top: 2rem;
    background-color: #0faf87;
  }
  button:hover {
    opacity: 0.7;
  }
</style>
