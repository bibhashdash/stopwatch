<template>
  <div class="timer elapsed">
    <div class="timer-title"><p class="timer-title-text">Elapsed</p></div>
    <p class="timer-text">
      <span>{{ elapsedMins }}</span
      >:<span>{{ elapsedSecs }}</span>
    </p>
  </div>
</template>

<script>
export default {
  name: "Elapsed",
  props: ["elapsedMins", "elapsedSecs"],
};
</script>

<style></style>
