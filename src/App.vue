<template>
  <AppCalculator />
</template>

<script>
import AppCalculator from "./components/AppCalculator.vue";

export default {
  name: "App",
  components: {
    AppCalculator,
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
  justify-content: center;
}
</style>
