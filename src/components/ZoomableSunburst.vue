<script setup>
import {nextTick, onMounted} from "vue";
import {createZoomableSunburst} from "../lib/zoomableSunburstChart.js";

onMounted(async () => {
  await nextTick();
  await createZoomableSunburst();
});
</script>

<template>
  <svg id="chart"></svg>
</template>

<style scoped>
</style>