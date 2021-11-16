<template>
  <section>

<div id="grid-container">
         <img
         src="@/assets/images/human-water-cycle-testing2-base-01.png"
          type="image/png"
          class="hwc"
        />
        <arrows class="hwc-arrows" />
        <labels class="hwc-labels" />
        <blobs class="hwc-blobs" />
    </div>
  </section>
</template>
<script>
import * as d3Base from 'd3';
import {drag} from "d3-drag@3";
import arrows from "@/assets/images/human-water-cycle-testing2-arrows-01.svg";
import labels from "@/assets/images/human-water-cycle-testing2-labels-01.svg";
import blobs from "@/assets/images/blobs-01.svg";
export default {
  name: "DragNDrop",
    components: {
        arrows, 
        labels, 
        blobs
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
      this.d3 = Object.assign(d3Base);

      // resize
      this.width = window.innerWidth //- this.margin.left - this.margin.right;
      this.height = window.innerHeight//*.5 - this.margin.top - this.margin.bottom;

      // define style before page fully loads
      this.svg = this.d3.select("#grid-container")
        .append('svg')
        .attr("viewBox", [0, 0, 2736, 1872])
    },
    methods:{
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
</style>