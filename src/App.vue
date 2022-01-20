<template>
  <h1>Stop Watch</h1>
  <h2>Start Training!</h2>
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
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-content: center;
}
</style>
