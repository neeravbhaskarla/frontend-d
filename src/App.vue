<template>
  <div>
    <NeuralBackground />
    <main style="position: relative; z-index: 2; color: white; text-align: center; padding: 3rem;">
      <h1>Hello Vue + Neural Background</h1>
      <p>This should float above the animated canvas.</p>
    </main>
  </div>
</template>

<script>
import NeuralBackground from "./components/NeuralBackground.vue";

export default {
  components: { NeuralBackground },
};
</script>
