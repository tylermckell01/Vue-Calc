<template>
  <CalculatorTitle :title="title" />
  <AppCalculator />
</template>

<script>
import CalculatorTitle from "./components/CalculatorTitle.vue";
import AppCalculator from "./components/AppCalculator.vue";

export default {
  name: "App",
  components: {
    AppCalculator,
    CalculatorTitle,
  },
  props: {
    title: {
      type: String,
      default: "Calculator",
    },
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
  align-items: center;
}
</style>
