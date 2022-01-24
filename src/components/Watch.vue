<template>
  <div class="watchcontainer">
    <div class="watch-face">
      <Prevlap :prevMins="prevMins" :prevSecs="prevSecs" />
      <Elapsed
        :elapsedMins="elapsedMins"
        :elapsedSecs="elapsedSecs"
        :lapCounter="lapCounter"
        :timerrunning="timerrunning"
      />
    </div>
    <div class="buttons-container">
      <button
        class="button start-button"
        :disabled="timerrunning"
        @click="startTimer"
      >
        <p>▶️</p>
        <p>Start</p>
      </button>
      <button
        class="button pause-button"
        :disabled="!timerrunning"
        @click="pauseTimer"
      >
        <p>⏸️</p>
        <p>Pause</p>
      </button>
      <button
        :disabled="timerrunning"
        class="button stop-button"
        @click="stopTimer"
      >
        <p>❌</p>
        <p>Stop</p>
      </button>
      <button
        @click="changeLap"
        class="button lap-button"
        :disabled="!timerrunning"
      >
        <p>🔁</p>
        <p>Lap</p>
      </button>
      <button
        @click="toggleLapsList"
        class="button laplist-button"
        :disabled="timerrunning"
      >
        <p>📃</p>
        <p>History</p>
      </button>
    </div>
  </div>
  <div class="lapslist-backdrop" v-if="showLapsList">
    <div class="lapslist-container">
      <ul>
        <li v-for="(prevlap, index) in prevLapsList" :key="prevlap">
          <p>
            Lap {{ index }} - <span>{{ prevlap[0] }}</span
            >:<span>{{ prevlap[1] }}</span>
          </p>
        </li>
      </ul>
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
      showLapsList: false,
    };
  },

  methods: {
    startTimer() {
      console.log("Watch has started!");
      this.timerrunning = !this.timerrunning;
      // console.log(`timerrunning property is set to ${this.timerrunning}`);

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
      // console.log(`timerrunning property is set to ${this.timerrunning}`);
      this.timerrunning = !this.timerrunning;
      clearInterval(this.timer);
    },

    stopTimer() {
      console.log("Watch has stopped!");
      this.timerrunning = false;
      // console.log(`timerrunning property is set to ${this.timerrunning}`);
      clearInterval(this.timer);
      this.elapsedMins = 0;
      this.elapsedSecs = 0;
      this.prevMins = 0;
      this.prevSecs = 0;
      this.lapCounter = 1;
      this.lapMarkersList = [[0, 0]];
      this.prevLapsList = [[0, 0]];
    },

    changeLap() {
      this.lapCounter++;
      // console.log("You're on lap number: ", this.lapCounter);

      this.lapMarkersList.push([this.elapsedMins, this.elapsedSecs]);
      // console.log("Lap Markers List", this.lapMarkersList);
      this.prevMins =
        this.lapMarkersList[this.lapCounter - 1][0] -
        this.lapMarkersList[this.lapCounter - 2][0];
      this.prevSecs =
        this.lapMarkersList[this.lapCounter - 1][1] -
        this.lapMarkersList[this.lapCounter - 2][1];
      // console.log(this.prevMins, this.prevSecs);
      this.prevLapsList.push([this.prevMins, this.prevSecs]);
    },
    toggleLapsList() {
      this.showLapsList = !this.showLapsList;
    },
  },
};
</script>

<style scoped>
body {
  /* margin: 0; */
  /* padding: 0; */
}
.watchcontainer {
  width: 320px;
  height: 500px;
  background-color: rgb(114, 114, 114);
  align-self: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  justify-content: space-evenly;
  border-radius: 2%;
}
.buttons-container {
  margin-top: 0.5rem;
  margin-bottom: 0.5rem;
  width: 90%;
  /* height: 15%; */
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 0.5rem;
}
.button {
  background-color: black;
  cursor: pointer;
  margin: 0;
  padding: 0;
  /* width: 100%; */
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  border-radius: 10px;
  border-style: none;
  font-family: "Quicksand", sans-serif;
}
.start-button {
  grid-column: 1 / 3;
  grid-row: 1;
  width: 100%;
}

.button p {
  color: #fff;
  /* font-size: 1rem; */
}
.button:active {
  background-color: lemonchiffon;
}
.button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
.watch-face {
  width: 90%;
  height: 60%;
  display: grid;
  grid-template-rows: repeat(2, 1fr);
  border-radius: 5%;
  background-color: black;
  justify-items: center;
  font-family: "Orbitron", sans-serif;
}
.timer {
  /* border-radius: 5%; */
  width: 90%;
}

.lapslist-backdrop {
  background-color: rgba(0, 0, 0, 0.308);
  width: 300px;
  align-self: center;
  display: flex;
  flex-direction: column;
  /* align-items: center; */
  position: relative;
  justify-content: space-evenly;
}
.lapslist-container {
  height: auto;
  z-index: 45;
  background-color: aliceblue;

  color: black;
}
ul {
  list-style: none;
}
</style>
