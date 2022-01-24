<template>
  <h2>List of laps</h2>
  <div class="list-container">
    <ol>
      <li>prevLapsList</li>
    </ol>
  </div>
</template>

<script>
import Watch from "./Watch.vue";
export default {
  name: "Lapslist",
  props: [],
  components: {
    Watch,
  },
  data() {
    return {
      prevLapsList,
    };
  },
};
</script>

<style></style>
