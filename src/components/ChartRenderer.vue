<template>
  <div>
    <Heatmap :chartData="chartData"/>
    <Boxplot :chartData="chartData"/>
  </div>
</template>

<script>
import Heatmap from "./Heatmap.vue";
import Boxplot from "./Boxplot.vue";

export default {
  name: "ChartRenderer",
  components: {
    Boxplot,
    Heatmap
  },
  mounted() {
    this.renderChartData();
  },
  data() {
    let chartData;
    return {
      chartData
    };
  },
  methods: {
    async renderChartData() {}
  }
};
</script>

