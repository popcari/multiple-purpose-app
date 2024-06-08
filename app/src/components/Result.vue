<template>
  <p>
    Reaction time: <strong>{{ timeScore }}</strong> ms
  </p>
  <p
    class="rank"
    :style="{ color: rankColor }"
  >
    {{ rank }}
  </p>
</template>

<script setup>
  import { ref, onMounted, defineProps } from 'vue';

  const props = defineProps({
    score: String,
  });
  const timeScore = ref(props.score);

  const rank = ref(null);
  const rankColor = ref('#0faf87');

  onMounted(() => {
    const scores = [
      { limit: 100, text: 'You are Flash !!!', color: '#0faf87' },
      { limit: 250, text: 'You are fast enough', color: '#276DE6' },
      { limit: 400, text: 'Rapid Reflexes', color: '#BAD60F' },
      { limit: 600, text: 'Not too bad...', color: '#EFAB19' },
      { limit: Infinity, text: 'Snail pace...', color: '#D6220F' },
    ];

    const score = scores.find((score) => timeScore.value < score.limit);
    rank.value = score.text;
    rankColor.value = score.color;
  });
</script>

<style>
  .rank {
    font-size: 1.4rem;
    font-weight: bold;
  }
</style>
