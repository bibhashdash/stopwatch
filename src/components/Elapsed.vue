<template>
  <div class="timer elapsed">
    <div class="timer-title"><p class="timer-title-text">Elapsed</p></div>

    <div class="timer-text">
      <p>{{ styleTimer(elapsedMins) }}:</p>

      <p class="secsDisplay">{{ styleTimer(elapsedSecs) }}</p>
    </div>
    <div class="lapNumberDisplay" v-if="timerrunning === true">
      Lap {{ lapCounter }} active
    </div>
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
.elapsed {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}
.lapNumberDisplay {
  color: rgb(233, 195, 27);
}
.timer-text {
  color: aliceblue;
  display: flex;
  flex-direction: row;
  justify-content: center;
  font-size: 1.5rem;
}
.timer-text p {
  width: 4rem;
  letter-spacing: 5px;
}
.secsDisplay::after {
  content: "s";
  font-size: 14px;
}
</style>
