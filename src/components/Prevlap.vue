<template>
  <div class="timer prev-lap">
    <div class="timer-title"><p class="timer-title-text">Prev Lap</p></div>
    <div class="timer-text">
      <p>{{ styleTimer(prevMins) }}:</p>
      <p class="secsDisplay">{{ styleTimer(prevSecs) }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Prevlap",

  props: ["prevMins", "prevSecs"],
  methods: {
    styleTimer(timerValue) {
      return ("0" + `${String(timerValue)}`).slice(-2);
    },
  },
};
</script>

<style></style>
