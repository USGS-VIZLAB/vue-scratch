<template>
  <section>
    <div id="grid-container">
      <img
        src="@/assets/images/human-water-cycle-testing2-base-01.png"
        type="image/png"
        class="hwc"
      >
      <arrows class="hwc-arrows" />
      <labels class="hwc-labels" />
      <blobs class="hwc-blobs" />
      <svg class="word-bank" />
    </div>
  </section>
</template>
<script>
import * as d3 from 'd3';
import {drag} from "d3-drag";
import arrows from "@/assets/images/human-water-cycle-testing2-arrows-01.svg";
import labels from "@/assets/images/human-water-cycle-testing2-labels-01.svg";
import blobs from "@/assets/images/blobs-01.svg";
import Vue from "vue";
export default {
  name: "DragNDrop",
    components: {
        arrows, 
        labels, 
        blobs
    },
    data() {
    return {
      publicPath: process.env.BASE_URL, // allows the application to find files in public folder when on different deployment roots
      //d3: null,

      // dimensions
      width: null,
      height: null,
      margin: { top: 50, right: 50, bottom: 50, left: 50 },
      svg: null,
      word_bank: null,
      radius: null, 

    }
  },
  mounted(){      
     // this.d3 = Object.assign(d3Base);
      Vue.nextTick(() => {
          d3.select("g")
          .datum({
              x: 0,
              y: 0,
          })
          .call(
              d3.drag().on("drag", function (d) {

                  d3.select(this).attr("transform", `translate(${d.x} , ${d.y})`);
              })
          );
      });

      // resize
      this.width = 2736 //- this.margin.left - this.margin.right;
      this.height = 1872//*.5 - this.margin.top - this.margin.bottom;
      this.radius = 32;

      this.word_bank = d3.select(".hwc-blobs")
        .append('g')
        //.attr("viewBox", [0, 0, this.width, this.height])
        .classed("word-bank-svg", true)

      this.makeDrops();
    
    },
    methods:{
        // add random points to svg
        makeDrops(){
            const self = this

            const circles = d3.range(100).map(i => ({
                x: Math.random() * (this.width - this.radius * 2) + this.radius,
                y: Math.random() * (this.height - this.radius * 2) + this.radius,
            }));

            this.word_bank.selectAll("circle")
                .data(circles)
                .join("circle")
                .attr("cx", d => d.x)
                .attr("cy", d => d.y)
                .attr("r", this.radius)
                .attr("fill", (d, i) => d3.schemeTableau10[i % 8])
                .attr("id", (d, i) => { return 'dot_' + i })
                .call((d, i) => self.drag(d, i));

            return this.word_bank.node();

        },
        // drag and drop dots
        drag(d, i){
            console.log(d, i)
            function dragstarted(event, d) {
                d3.select(this).raise().attr("stroke", "black");
            }

        function dragged(event, d) {
                d3.select(this).attr("cx", d.x = event.x).attr("cy", d.y = event.y);
            }

        function dragended(event, d) {
                d3.select(this).attr("stroke", null);
            }

        return d3.drag()
            .on("start", dragstarted)
            .on("drag", dragged)
            .on("end", dragended);

        }
    }
}
</script>
<style scoped lang="scss">

#grid-container {
    display: grid;
    grid-template-rows: 1fr;
    grid-template-columns: 5vw 1fr 5vw;
}
.hwc {
    max-width: 100%;
    max-height: 100%;
    grid-row: 1 / 2;
    grid-column: 2 / 2;
    z-index: 0;
}
.hwc-arrows {
    max-width: 100%;
    max-height: 100%;
    grid-row: 1 / 2;
    grid-column: 2 / 2;
    z-index: 1;
}
.hwc-labels {
    max-width: 100%;
    max-height: 100%;
    grid-row: 1 / 2;
    grid-column: 2 / 2;
    z-index: 2;
}
.hwc-blobs {
    max-width: 100%;
    max-height: 100%;
    grid-row: 1 / 2;
    grid-column: 2 / 2;
    z-index: 5;
}
.word-bank {
    max-width: 100%;
    max-height: 100%;
    grid-row: 1 / 2;
    grid-column: 2 / 2;
    z-index: 6;
}
.word-bank-svg {
    fill: blue;
}
</style>