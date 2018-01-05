<template>
  <div id="app">
    <h1>Vue Timeslot</h1>
    <p>A tiny timeslot selector with no dependencies!</p>
    <VueTimeSlot :min="4"  @callback="selectedSlot" ></VueTimeSlot>
  </div>
</template>

<script>
import VueTimeSlot from "./components/VueTimeSlot";

export default {
  name: "app",
  methods: {
    selectedSlot(val) {
      console.log(val);
    }
  },
  components: {
    VueTimeSlot
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
