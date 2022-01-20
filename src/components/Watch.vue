<template>
  <div class="watchcontainer">
    <div class="buttons-container">
      <div class="button start-button"><p>✅</p></div>
      <div class="button stop-button"><p>❌</p></div>
    </div>

    <div class="watch-face"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },

  methods: {},
};
</script>

<style scoped>
.watchcontainer {
  width: 500px;
  height: 500px;
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
}
</style>
