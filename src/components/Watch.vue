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
        <p><i class="fas fa-play"></i></p>
        <p>Start</p>
      </button>
      <button
        class="button pause-button"
        :disabled="!timerrunning"
        @click="pauseTimer"
      >
        <p><i class="fas fa-pause"></i></p>
        <p>Pause</p>
      </button>
      <button
        :disabled="timerrunning"
        class="button stop-button"
        @click="stopTimer"
      >
        <p><i class="fas fa-times"></i></p>
        <p>Clear</p>
      </button>
      <button
        @click="changeLap"
        class="button lap-button"
        :disabled="!timerrunning"
      >
        <p><i class="fas fa-redo"></i></p>
        <p>Lap</p>
      </button>
      <button
        @click="toggleLapsList"
        class="button laplist-button"
        :disabled="timerrunning"
      >
        <p><i class="fas fa-clipboard-list"></i></p>
        <p>Log</p>
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
          this.elapsedMins++;
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
  height: 520px;
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
  justify-content: center;
  border-radius: 10px;
  border-style: none;
  font-family: "Quicksand", sans-serif;
  letter-spacing: 2px;
}
.fas {
  margin-right: 10px;
  font-size: 1rem;
}
.fa-play {
  color: green;
}
.fa-pause {
  color: rgb(0, 93, 216);
}
.fa-times {
  color: red;
}
.fa-redo {
  color: rgb(233, 195, 27);
}
.fa-clipboard-list {
  color: lightslategray;
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
.button:hover {
  background-color: rgba(0, 0, 0, 0.787);
}
.button:active {
  background-color: lemonchiffon;
}
.button:disabled {
  opacity: 0.2;
  cursor: not-allowed;
}
.watch-face {
  width: 90%;
  height: 70%;
  display: grid;
  grid-template-rows: repeat(2, 1fr);
  border-radius: 5%;
  background-color: black;
  justify-items: center;
  font-family: "Orbitron", sans-serif;
  letter-spacing: 2px;
}
.timer {
  /* border-radius: 5%; */
  width: 90%;
}

.lapslist-backdrop {
  /* background-color: rgba(146, 96, 96, 0.308); */
  width: 320px;

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
  background-color: rgb(94, 178, 251);
  border-radius: 10px;
  color: #fff;
}
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
