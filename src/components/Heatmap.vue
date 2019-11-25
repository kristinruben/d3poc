<template>
  <div class="hello">
    <div id="heatmap"/>
  </div>
</template>

<script>
import * as d3 from "d3";

export default {
  name: "Heatmap",
  props: {
    chartData: {
      type: Object
    }
  },
  mounted() {
    this.grabData();
  },
  data() {
    const width = 800;
    const height = 200;
    const margin = { top: 80, right: 100, bottom: 70, left: 60 };
    const tableData = [
      { row: "CD38", value: 3.4874078000744313, column: "Prostate" },
      { row: "CD38", value: 0.23794745147999544, column: "Skin" },
      { row: "CD38", value: -0.2679986393608747, column: "Bladder" },
      { row: "CD38", value: -0.2652058087914437, column: "Breast" },
      { row: "CD38", value: -0.227570767926003, column: "Stomach" },
      { row: "ICOS", value: -0.2810212053349176, column: "Prostate" },
      { row: "ICOS", value: -0.17797198018665505, column: "Skin" },
      { row: "ICOS", value: -0.23247797377089743, column: "Bladder" },
      { row: "ICOS", value: -0.2714372959761951, column: "Breast" },
      { row: "ICOS", value: -0.2713121395032097, column: "Stomach" },
      { row: "Granzyme B", value: -0.2716878419882237, column: "Prostate" },
      { row: "Granzyme B", value: -0.11706272973313565, column: "Skin" },
      { row: "Granzyme B", value: -0.2791070338030194, column: "Bladder" },
      { row: "Granzyme B", value: -0.29152945467848224, column: "Breast" },
      { row: "Granzyme B", value: -0.27674048105312354, column: "Stomach" },
      { row: "CD28", value: 0.6500905138137167, column: "Prostate" },
      { row: "CD28", value: 2.886813117069073, column: "Skin" },
      { row: "CD28", value: 0.3579832301116793, column: "Bladder" },
      { row: "CD28", value: 0.07444112403015335, column: "Breast" },
      { row: "CD28", value: 0.1502183575025921, column: "Stomach" },
      { row: "NKp46", value: -0.28351664361472206, column: "Prostate" },
      { row: "NKp46", value: -0.20654890871954668, column: "Skin" },
      { row: "NKp46", value: -0.29837227413258327, column: "Bladder" },
      { row: "NKp46", value: -0.29740738065370115, column: "Breast" },
      { row: "NKp46", value: -0.29655389275040017, column: "Stomach" },
      { row: "CD45", value: -0.12721811706534092, column: "Prostate" },
      { row: "CD45", value: 0.10707526649550388, column: "Skin" },
      { row: "CD45", value: -0.1559411780164111, column: "Bladder" },
      { row: "CD45", value: -0.19457420774092743, column: "Breast" },
      { row: "CD45", value: -0.08116356486545194, column: "Stomach" },
      { row: "CD137", value: -0.286162176435686, column: "Prostate" },
      { row: "CD137", value: -0.15338397723131586, column: "Skin" },
      { row: "CD137", value: -0.26221090994998597, column: "Bladder" },
      { row: "CD137", value: -0.27796524318634214, column: "Breast" },
      { row: "CD137", value: -0.25154440875324235, column: "Stomach" },
      { row: "LAG3", value: -0.2944651547412839, column: "Prostate" },
      { row: "LAG3", value: -0.23892737771959927, column: "Skin" },
      { row: "LAG3", value: -0.29230672998091495, column: "Bladder" },
      { row: "LAG3", value: -0.29152386109309736, column: "Breast" },
      { row: "LAG3", value: -0.2865087456634874, column: "Stomach" },
      { row: "FOXP3", value: -0.28627801026636346, column: "Prostate" },
      { row: "FOXP3", value: -0.1575323199923358, column: "Skin" },
      { row: "FOXP3", value: -0.29042751835767194, column: "Bladder" },
      { row: "FOXP3", value: -0.2872501287930343, column: "Breast" },
      { row: "FOXP3", value: -0.28440159543581284, column: "Stomach" },
      { row: "PSGL1", value: -0.1599722885504075, column: "Prostate" },
      { row: "PSGL1", value: 0.25720103850667436, column: "Skin" },
      { row: "PSGL1", value: -0.1582879201514024, column: "Bladder" },
      { row: "PSGL1", value: -0.13390035400568603, column: "Breast" },
      { row: "PSGL1", value: -0.1307581574157613, column: "Stomach" },
      { row: "TIGIT", value: -0.12214753191399821, column: "Prostate" },
      { row: "TIGIT", value: -0.13022233854910673, column: "Skin" },
      { row: "TIGIT", value: -0.21560002907036466, column: "Bladder" },
      { row: "TIGIT", value: -0.2210528425563371, column: "Breast" },
      { row: "TIGIT", value: -0.23704933142664464, column: "Stomach" },
      { row: "VISTA", value: 0.03152783615595832, column: "Prostate" },
      { row: "VISTA", value: -0.05117681974952698, column: "Skin" },
      { row: "VISTA", value: -0.22990818741868627, column: "Bladder" },
      { row: "VISTA", value: -0.26534634762423737, column: "Breast" },
      { row: "VISTA", value: -0.266891575586795, column: "Stomach" },
      { row: "CD39", value: 1.035066930329695, column: "Prostate" },
      { row: "CD39", value: 1.1056360696767473, column: "Skin" },
      { row: "CD39", value: 0.30194249653747596, column: "Bladder" },
      { row: "CD39", value: 0.543476077180802, column: "Breast" },
      { row: "CD39", value: 0.3212874454587736, column: "Stomach" },
      { row: "CCR2", value: -0.12822682696307083, column: "Prostate" },
      { row: "CCR2", value: -0.09661304769833524, column: "Skin" },
      { row: "CCR2", value: -0.27413573479225717, column: "Bladder" },
      { row: "CCR2", value: -0.25888272664601575, column: "Breast" },
      { row: "CCR2", value: -0.2573421600046123, column: "Stomach" },
      { row: "NKG2D", value: 0.1981933740179373, column: "Prostate" },
      { row: "NKG2D", value: 0.25082598263037903, column: "Skin" },
      { row: "NKG2D", value: -0.08024458539993695, column: "Bladder" },
      { row: "NKG2D", value: -0.057363791317257495, column: "Breast" },
      { row: "NKG2D", value: 0.018452364186817317, column: "Stomach" },
      { row: "CD3", value: -0.08957864794480391, column: "Prostate" },
      { row: "CD3", value: 0.03812873304216579, column: "Skin" },
      { row: "CD3", value: -0.191255580145323, column: "Bladder" },
      { row: "CD3", value: -0.2318253888093346, column: "Breast" },
      { row: "CD3", value: -0.1485758244609444, column: "Stomach" },
      { row: "CD8", value: -0.12826085460749517, column: "Prostate" },
      { row: "CD8", value: 0.04142894841921183, column: "Skin" },
      { row: "CD8", value: -0.19206315403525695, column: "Bladder" },
      { row: "CD8", value: -0.23726305300155653, column: "Breast" },
      { row: "CD8", value: -0.1643802668997063, column: "Stomach" },
      { row: "CD33", value: 0.6312900072032084, column: "Prostate" },
      { row: "CD33", value: 1.387750413088797, column: "Skin" },
      { row: "CD33", value: 0.3848035397676786, column: "Bladder" },
      { row: "CD33", value: 0.35790958123744576, column: "Breast" },
      { row: "CD33", value: 0.10182288981915433, column: "Stomach" },
      { row: "CD163+CD68", value: 0.1185080888899683, column: "Prostate" },
      { row: "CD163+CD68", value: 0.2981754498468548, column: "Skin" },
      { row: "CD163+CD68", value: 0.03945720957106145, column: "Bladder" },
      { row: "CD163+CD68", value: -0.1006476542231971, column: "Breast" },
      { row: "CD163+CD68", value: -0.1206237460287491, column: "Stomach" },
      { row: "PD1", value: -0.21274077467448893, column: "Prostate" },
      { row: "PD1", value: -0.16897959248237762, column: "Skin" },
      { row: "PD1", value: -0.27340180977655676, column: "Bladder" },
      { row: "PD1", value: -0.2876621895830497, column: "Breast" },
      { row: "PD1", value: -0.2791725253652333, column: "Stomach" }
    ];
    const heatColor = d3.interpolateRdBu;
    return {
      width,
      height,
      tableData,
      margin,
      heatColor
    };
  },
  computed: {},
  methods: {
    async grabData() {
      // append the svg object to the body of the page
      const svg = d3
        .select("#heatmap")
        .append("svg")
        .attr("width", this.width + this.margin.left + this.margin.right)
        .attr(
          "height",
          +60 + this.height + this.margin.top + this.margin.bottom
        )
        .append("g")
        .attr(
          "transform",
          "translate(" + this.margin.left + "," + this.margin.top + ")"
        );

      const myGroups = d3.map(this.tableData, d => d.row).keys();
      const myVars = d3.map(this.tableData, d => d.column).keys();

      const x = d3
        .scaleBand()
        .range([0, this.width])
        .domain(myGroups)
        .padding(0.05);
      svg
        .append("g")
        .style("font-size", 12)
        .attr("class", "axis")
        .attr("transform", `translate(0, ${this.height})`)
        .call(d3.axisBottom(x).tickSize(0))
        .selectAll("text")
        .style("text-anchor", "end")
        .attr("transform", "rotate(-45)")
        .on("mouseover", function(d, i) {
          d3.select(this)
            .style("text-decoration", "underline")
            .style("cursor", "pointer");
        })
        .on("mouseout", function(d, i) {
          d3.select(this).style("text-decoration", "none");
        })
        .on("click", (d, i) => console.log(`Clicked on ${d}`)); //
      svg.select(".domain").remove();
      //Read the data

      // Build Y scales and axis:
      const y = d3
        .scaleBand()
        .range([this.height, 0])
        .domain(myVars)
        .padding(0.05);
      svg
        .append("g")
        .style("font-size", 12)
        .call(d3.axisLeft(y).tickSize(0))
        .select(".domain")
        .remove();
      svg
        .selectAll("text")
        .on("mouseover", function(d, i) {
          d3.select(this)
            .style("text-decoration", "underline")
            .style("cursor", "pointer");
        })
        .on("mouseout", function(d, i) {
          d3.select(this).style("text-decoration", "none");
        })
        .on("click", (d, i) => console.log(`Clicked on ${d}`));

      // Build color scale
      const myColor = d3
        .scaleSequential()
        .interpolator(this.heatColor)
        .domain([3, -3]);

      // create a tooltip
      const tooltip = d3
        .select("#heatmap")
        .append("div")
        .style("opacity", 0)
        .attr("width", "100%")
        .attr("class", "tooltip")
        .style("background-color", "white")
        .style("border", "solid")
        .style("border-width", "2px")
        .style("border-radius", "5px")
        .style("padding", "5px");

      // Three function that change the tooltip when user hover / move / leave a cell
      const mouseover = function(d) {
        tooltip.style("opacity", 1);
        d3.select(this)
          .style("stroke", "black")
          .html("value: " + d.value)
          .style("top", d3.mouse(d3.event.pageY) + "px");
      };
      const mousemove = d =>
        tooltip
          .html(
            `value: ${d.value} -- indication: ${d.column} -- biomarker: ${
              d.row
            }`
          )
          .style("left", `${d3.mouse(d3.event.pageX) + 70}px`)
          .style("top", d3.mouse(d3.event.pageY) + "px");
      const mouseleave = function(d) {
        tooltip.style("opacity", 0);
        d3.select(this).style("stroke", "none");
      };

      // add the squares
      svg
        .selectAll()
        .data(this.tableData, function(d) {
          return d.row + ":" + d.column;
        })
        .enter()
        .append("rect")
        .attr("x", function(d) {
          return x(d.row);
        })
        .attr("y", function(d) {
          return y(d.column);
        })
        .attr("rx", 4)
        .attr("ry", 4)
        .attr("width", x.bandwidth())
        .attr("height", y.bandwidth())
        .style("fill", function(d) {
          return myColor(d.value);
        })
        .style("stroke-width", 2)
        .style("stroke", "none")
        .on("mouseover", mouseover)
        .on("mousemove", mousemove)
        .on("mouseleave", mouseleave);

      // Add title to graph
      svg
        .append("text")
        .attr("x", 0)
        .attr("y", -50)
        .attr("text-anchor", "left")
        .style("font-size", "22px")
        .text("MTB POC");

      // Add subtitle to graph
      svg
        .append("text")
        .attr("x", 0)
        .attr("y", -20)
        .attr("text-anchor", "left")
        .style("font-size", "14px")
        .style("fill", "grey")
        .style("max-width", 400)
        .text("Made in D3.js and Vue.js");

      // create a legend
      const legend = svg
        .selectAll(".legend")
        .data([-2, -1, 0, 1, 2, 3])
        .enter()
        .append("g")
        .attr("class", "legend");

      legend
        .append("rect")
        .attr("y", function(d, i) {
          return 36 * i + 2;
        })
        .attr("x", this.width + 10)
        .attr("width", "36px")
        .attr("height", "36px")
        .style("fill", function(d, i) {
          return myColor(d);
        });
    }
  }
};
</script>

<style scoped>
.hello {
  width: 100%;
}

.legend {
  width: 100%;
  height: 100%;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
