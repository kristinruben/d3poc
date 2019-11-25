<template>
  <div id="app">
    <ChartRenderer/>
  </div>
</template>

<script>
import ChartRenderer from "./components/ChartRenderer";

export default {
  name: "App",
  components: {
    ChartRenderer
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
