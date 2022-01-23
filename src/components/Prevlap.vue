<template>
  <div class="timer prev-lap">
    <div class="timer-title"><p class="timer-title-text">Prev Lap</p></div>
    <p class="timer-text">
      <span>{{ prevMins }}</span
      >:<span>{{ prevSecs }}</span>
    </p>
  </div>
</template>

<script>
export default {
  name: "Prevlap",

  props: ["prevMins", "prevSecs"],
};
</script>

<style>
.timer-text {
  font-size: 2.5rem;
  color: aliceblue;
}
</style>
