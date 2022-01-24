<template>
  <div class="timer elapsed">
    <div class="timer-title"><p class="timer-title-text">Elapsed</p></div>

    <p class="timer-text">
      <span>{{ styleTimer(elapsedMins) }}</span
      >:<span>{{ styleTimer(elapsedSecs) }}</span>
    </p>
    <p class="lapNumberDisplay" v-if="timerrunning === true">
      Lap {{ lapCounter }} active
    </p>
  </div>
</template>

<script>
export default {
  name: "Elapsed",
  props: ["elapsedMins", "elapsedSecs", "lapCounter", "timerrunning"],

  methods: {
    styleTimer(timerValue) {
      return ("0" + `${String(timerValue)}`).slice(-2);
    },
  },
};
</script>

<style>
.lapNumberDisplay {
  color: rgb(233, 195, 27);
}
.timer-text p,
.timer-text span {
  font-size: 2rem;
  color: aliceblue;
}
.timer-text span {
  margin: 1rem;
  width: 80px;
}
</style>
