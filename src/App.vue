<script setup lang="ts">
import EmblaCarousel from './components/EmblaCarousel.vue'
</script>

<template>
  <div class="split-container">
    <div class="horizontal-container">
      <EmblaCarousel axis="x" />
    </div>
    <div class="vertical-container">
      <EmblaCarousel axis="y" />
    </div>
  </div>
</template>

<style scoped>
.split-container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width: 100vw;
}

.horizontal-container {
    flex: 3;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
    width: 100%;
}

.vertical-container {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
}
</style>
