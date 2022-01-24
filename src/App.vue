<template>
  <h1>Stop Watch</h1>

  <Watch />
</template>

<script>
import Watch from "./components/Watch.vue";

export default {
  name: "App",
  components: {
    Watch,
  },
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #dae1e9;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-content: center;
  font-family: "Montserrat", sans-serif;
  font-family: "Orbitron", sans-serif;
  font-family: "Quicksand", sans-serif;
}
h1,
h2 {
  color: darkslategrey;
}
</style>
