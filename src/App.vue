<template>
  <div>
    <NeuralBackground />
    <main style="position: relative; z-index: 2; color: white; text-align: center; padding: 3rem;">
      <Login/>
    </main>
  </div>
</template>

<script>
import NeuralBackground from "./components/NeuralBackground.vue";
import Login from "./components/Login.vue"

export default {
  components: { NeuralBackground, Login},
};
</script>
