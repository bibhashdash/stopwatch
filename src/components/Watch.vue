<template>
  <div class="watchcontainer">
    <div class="buttons-container">
      <button
        class="button start-button"
        :disabled="timerrunning"
        @click="startTimer"
      >
        <p>✅</p>
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
      <button @click="changeLap" class="button lap-button" disabled>
        <p>🔁</p>
      </button>
    </div>

    <div class="watch-face">
      <div class="timer prev-lap">
        <div class="timer-title"><p class="timer-title-text">Prev Lap</p></div>
        <p class="timer-text">00:00</p>
      </div>
      <div class="timer elapsed">
        <div class="timer-title"><p class="timer-title-text">Elapsed</p></div>
        <p class="timer-text">
          <span>{{ elapsed[0] }}</span
          >:<span>{{ elapsed[1] }}</span>
        </p>
      </div>

      <div class="timer curr-lap">
        <div class="timer-title"><p class="timer-title-text">Curr Lap</p></div>
        <p class="timer-text">00:00</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      prevLap: [0, 0],
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
        if (this.elapsed[1] === 59) {
          this.elapsed[0]++;
          this.elapsed[1] = 0;
        } else {
          this.elapsed[1]++;
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
      this.elapsed = [0, 0];
    },
    changeLap() {
      console.log("You're on a new lap!");
      // this.timerrunning = !this.timerrunning;
      console.log(`timerrunning property is set to ${this.timerrunning}`);
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
  width: 300px;
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
