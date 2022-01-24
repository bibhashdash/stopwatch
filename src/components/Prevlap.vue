<template>
  <div class="timer prev-lap">
    <div class="timer-title"><p class="timer-title-text">Prev Lap</p></div>
    <p class="timer-text">
      <span>{{ styleTimer(prevMins) }}</span> :
      <span>{{ styleTimer(prevSecs) }}</span>
    </p>
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

<style>
.timer-text span {
  font-size: 2rem;
  color: aliceblue;
}
</style>
