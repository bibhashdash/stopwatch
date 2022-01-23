<template>
  <div class="watchcontainer">
    <div class="buttons-container">
      <button
        class="button start-button"
        :disabled="timerrunning"
        @click="startTimer"
      >
        <p>▶️</p>
      </button>
      <button
        class="button pause-button"
        :disabled="!timerrunning"
        @click="pauseTimer"
      >
        <p>⏸️</p>
      </button>
      <button
        :disabled="timerrunning"
        class="button stop-button"
        @click="stopTimer"
      >
        <p>❌</p>
      </button>
      <button
        @click="changeLap"
        class="button lap-button"
        :disabled="!timerrunning"
      >
        <p>🔁</p>
      </button>
    </div>

    <div class="watch-face">
      <Prevlap :prevMins="prevMins" :prevSecs="prevSecs" />
      <Elapsed :elapsedMins="elapsedMins" :elapsedSecs="elapsedSecs" />
    </div>
  </div>
</template>

<script>
import Prevlap from "./Prevlap.vue";
import Elapsed from "./Elapsed.vue";
export default {
  name: "Watch",
  components: {
    Prevlap,
    Elapsed,
  },
  data() {
    return {
      lapMarkersList: [[0, 0]],
      prevLapsList: [[0, 0]],
      prevMins: 0,
      prevSecs: 0,
      elapsedMins: 0,
      elapsedSecs: 0,
      // lapChange: false,
      lapCounter: 1,
      elapsed: [0, 0],
      currLap: [0, 0],
      timerrunning: false,
      timer: null,
    };
  },

  methods: {
    startTimer() {
      console.log("Watch has started!");
      this.timerrunning = !this.timerrunning;
      console.log(`timerrunning property is set to ${this.timerrunning}`);

      this.timer = setInterval(() => {
        if (this.elapsedSecs === 59) {
          this.elapsedMins = 0;
          elapsedSecs++;
          this.elapsedSecs = 0;
        } else {
          this.elapsedSecs++;
        }
      }, 1000);
    },

    pauseTimer() {
      console.log("Watch has paused");
      console.log(`timerrunning property is set to ${this.timerrunning}`);
      this.timerrunning = !this.timerrunning;
      clearInterval(this.timer);
    },

    stopTimer() {
      console.log("Watch has stopped!");
      this.timerrunning = false;
      console.log(`timerrunning property is set to ${this.timerrunning}`);
      clearInterval(this.timer);
      this.elapsedMins = 0;
      this.elapsedSecs = 0;
      this.prevMins = 0;
      this.prevSecs = 0;
      this.lapCounter = 1;
    },

    changeLap() {
      this.lapCounter++;
      console.log("You're on lap number: ", this.lapCounter);

      this.lapMarkersList.push([this.elapsedMins, this.elapsedSecs]);
      console.log("Lap Markers List", this.lapMarkersList);
      this.prevMins =
        this.lapMarkersList[this.lapCounter - 1][0] -
        this.lapMarkersList[this.lapCounter - 2][0];
      this.prevSecs =
        this.lapMarkersList[this.lapCounter - 1][1] -
        this.lapMarkersList[this.lapCounter - 2][1];
      console.log(this.prevMins, this.prevSecs);
      this.prevLapsList.push([this.prevMins, this.prevSecs]);
      console.log("Prev laps List", this.prevLapsList);
      // prevMins: 0,
      // prevSecs: 0,
      // elapsedMins: 0,
      // elapsedSecs: 0,
      //   this.lapChange = true;

      //   console.log(`timerrunning property is set to ${this.timerrunning}`);
      //   this.prevLap[this.lapCounter] = [this.elapsed[0], this.elapsed[1]];
      //   this.lapCounter++;
    },
  },
};
</script>

<style scoped>
body {
  margin: 0;
  padding: 0;
}
.watchcontainer {
  width: 320px;
  height: 600px;
  background-color: rgb(245, 208, 208);
  align-self: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.buttons-container {
  width: 80%;
  height: 10%;
  display: flex;
  justify-content: space-evenly;
}
.button {
  width: 50px;
  height: 50px;
  background-color: black;
  cursor: pointer;
}
.button:active {
  background-color: lemonchiffon;
}
.watch-face {
  width: 90%;
  height: 90%;
  display: grid;
  grid-template-rows: repeat(3, 1fr);
  /* border-radius: 5%; */
}
.timer {
  background-color: black;
  /* border-radius: 5%; */
}
.timer-text {
  font-size: 2.5rem;
  color: aliceblue;
}
</style>
