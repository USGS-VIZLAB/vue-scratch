<template>
  <section>
    <div id="grid-container">
      <div id="map-container">
        <DAsvg
          id="map_gwl"
          class="map"
        />
      </div>
    </div>
  </section>
</template>
<script>
import * as d3Base from 'd3';
import DAsvg from "@/assets/dasvg-01-01.svg";
import { TimelineMax } from "gsap/all"; 

export default {
  name: "GWLsvg",
    components: {
      DAsvg
    },
    data() {
    return {
      publicPath: process.env.BASE_URL, // this is need for the data files in the public folder, this allows the application to find the files when on different deployment roots
      d3: null,

      // dimensions
      width: null,
      height: null,
      margin: { top: 50, right: 50, bottom: 50, left: 50 },

    }
  },
  mounted(){
      this.$gsap.registerPlugin(Draggable); // register gsap plugins for scrollTrigger 
      this.d3 = Object.assign(d3Base);


      // resize
      this.width = window.innerWidth - this.margin.left - this.margin.right;
      this.height = window.innerHeight*.5 - this.margin.top - this.margin.bottom;


      // define style before page fully loads
      this.svg = this.d3.select("svg.map")
      this.svg.selectAll(".map-bkgrd")
        .style("stroke", "grey")
        .style("stroke-width", "1px")
        .style("fill", "white")

        this.d3.selectAll(".curve")
        .style("opacity", 0)
        .attr("stroke", "#606060")

        this.d3.selectAll(".legend")
        .style("opacity", 0)
        .attr("stroke", "#606060")

         this.d3.selectAll(".leg_text_true")
        .style("opacity", 0)
        this.d3.selectAll(".leg_text_obs")
        .style("opacity", 0)
        this.d3.selectAll(".leg_text_pred")
        .style("opacity", 0)
        this.d3.selectAll(".leg_text_up")
        .style("opacity", 0)

        this.d3.selectAll(".legend")
        .style("opacity", 0)

        this.d3.select("#trend")
        .attr("stroke-dashoffset", -500)
        .style("opacity", 0)

        this.d3.selectAll(".pred")
        .attr("fill", "transparent")

        this.d3.selectAll(".up")
        .attr("fill", "transparent")

        this.d3.selectAll(".up")
        .attr("fill", "transparent")

        this.d3.select("#legend_up")
        .attr("fill", "#909090")
        .attr("stroke", "#606060")

         this.d3.select("#legend_obs")
        .attr("stroke", "#606060")

            this.d3.select("#legend_pred")
        .attr("stroke", "#606060")

        this.d3.select("#legend_true")
        .attr("stroke", "#33c780")

        //set up timeline animation
        this.initTime();

    },
    methods:{
      initTime(){
        var tl = new TimelineMax({ repeat: -1}) //TimelineMax permits repeating animation
 
        var time = 1.2;
        var alpha = 0.8;
        tl
        .to("#t0_pred", {opacity: alpha, duration: time}, 1)
        .to(".leg_text_pred", {opacity: alpha, duration: time}, 1)
        .to("#legend_pred", {opacity: alpha, duration: time}, 1)
        .to("#t1_pred", {opacity: alpha, duration: time}, 2)
        .to(".leg_text_obs", {opacity: alpha, duration: time}, 3)
        .to("#legend_obs", {opacity: alpha, duration: time}, 3)
        .to("#t1_obs", {opacity: 0.8, duration: time}, 3)
        .to(".leg_text_up", {opacity: alpha, duration: time}, 4)
        .to("#legend_up", {opacity: alpha, duration: time}, 4)
        .to("#t1_pred", {y: 0, scaleY:0.44, scaleX: 2.2, fill: "#909090",duration: time}, 4) // to t1 model update
        .to("#t2_pred", {opacity: alpha, duration: time}, 5)
        .to("#t3_pred", {opacity: alpha, duration: time}, 6)
        .to("#t4_pred", {opacity: alpha, duration: time}, 7)
        .to("#t4_obs", {opacity: 0.8, duration: time}, 8)
        .to("#t4_pred", {y: 15, x:-5, scaleY:0.48, scaleX: 1.8, fill: "#909090", duration: time}, 9) // to model update
        .to("#t5_pred", {opacity: alpha, duration: time}, 10)
        .to("#t6_pred", {opacity: alpha, duration: time}, 11)
        .to("#trend", {opacity: alpha, duration: time}, 12)
        .to("#legend_true", {opacity: alpha, duration: time}, 12)
        .to(".leg_text_true", {opacity: alpha, duration: time}, 12)
        .to(".leg_text_true", {opacity: alpha, duration: time}, 13)
        .to(".leg_text_true", {opacity: alpha, duration: time}, 14)

      }
    }
}
</script>
<style scoped lang="scss">
#map-container{
  width: auto;
  //height: 85vh;
  margin-left: 5%;
  margin-top: 2%;
  margin-bottom: 0;
  position: relative;
  grid-area: map;

    .map {
    position: relative;
    left:0;
    top: 0;
    width: 90vw;
    max-width: 1000px;
    max-height: 600px;
    height: auto;

  }
}

</style>