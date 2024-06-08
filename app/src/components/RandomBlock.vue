<template>
  <div class="random__block--container">
    <div
      class="block"
      v-if="showBlock"
      @click="stopTimer"
      :style="{
        width: btnWidthRandom + 'px',
        height: btnHeightRandom + 'px',
        right: rightRandom + 'rem',
        top: topRandom + 'rem',
      }"
    >
      <p class="click-me--btn">Click me</p>
      <p>{{ `${btnWidthRandom}px x ${btnHeightRandom}px` }}</p>
    </div>
  </div>
</template>

<script setup>
  import { ref, defineProps, defineEmits, onMounted } from 'vue';
  const props = defineProps({
    delay: Number,
  });

  const emit = defineEmits(['end']);
  const delayValue = ref(props.delay);
  const showBlock = ref(false);
  const timer = ref(null);
  const reactionTime = ref(null);

  const btnWidthRandom = ref(0);
  const btnHeightRandom = ref(0);
  const rightRandom = ref(10);
  const topRandom = ref(10);

  onMounted(() => {
    btnWidthRandom.value = getRandomNumber(60, 200);
    btnHeightRandom.value = getRandomNumber(50, 150);
    rightRandom.value = getRandomNumber(0, 60);
    topRandom.value = getRandomNumber(0, 30);

    setTimeout(() => {
      showBlock.value = true;
      startTimer();
    }, delayValue.value);
  });

  function getRandomNumber(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
  }

  function startTimer() {
    timer.value = setInterval(() => {
      reactionTime.value += 10;
    }, 10);
  }

  function stopTimer() {
    clearInterval(timer.value);

    emit('end', reactionTime.value);
  }
</script>

<style>
  .random__block--container {
    overflow: hidden;
    width: 100%;
    height: calc(100vh - 12rem);
    border: 2px dashed #7d7d7d;
    box-sizing: border-box;
    position: relative;
  }
  .block {
    position: absolute;
    border-radius: 20px;
    background: #0faf87;
    color: white;
    align-items: center;
    padding: 2rem;
    width: fit-content;
  }
  .click-me--btn {
    margin-bottom: 1rem;
    text-align: center;
  }
  p {
    padding: 0;
    margin: 0;
  }
  button {
    padding: 10px 30px;
    background: #333;
    color: white;
    font-weight: 600;
    border-radius: 5px;
    cursor: pointer;
  }
  button[disabled] {
    opacity: 0.2;
    cursor: not-allowed;
  }
</style>
