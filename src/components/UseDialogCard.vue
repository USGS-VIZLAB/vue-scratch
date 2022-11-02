<template>
  <div id='page-content'>
    <div id='svg-container'>
    </div>
    <div id="dialog-card-setup">
      <dialogCard 
          :show="showDialog"
          :header="cardHeader"
          :title="cardTitle"
          :text="cardText"
          :source="cardImageSource"
          :altText="cardAltText"
          :close="close"
        />
    </div>
  </div>
</template>

<script>
import * as d3Base from 'd3';
export default {
    name: 'useDialogCard',
    components: {
      dialogCard: () => import( /* webpackPreload: true */ /*webpackChunkName: "section"*/ "./../components/Dialog")
    },
    data() {
      return {
        publicPath: process.env.BASE_URL,
        d3: null,
        svg:  null,
        svgGroup: null,
        dialogData: null,
        showDialog: false,
        cardHeader: null,
        cardTitle: null,
        cardText: null,
        cardImageSource: null,
        cardAltText: null
      }
    },
    mounted(){
      this.d3 = Object.assign(d3Base);

      // create svg that will hold chart
      this.svg = this.d3.select("#svg-container").append("svg")
        .attr("viewBox", "0 0 600 400")
        .attr("preserveAspectRatio", "xMidYMid meet")
        .attr("width", '100%')
        .attr("height", '100%')

      this.svgGroup = this.svg.append("g")
        .attr("id", "svg-group")

      this.loadData();
    },
    methods:{
      close() {
        this.showDialog = false;
      },
      loadData(){
        const self = this;

        // read in data
        let promises = [
            self.d3.csv(self.publicPath + "data/dialog_data.csv", this.d3.autoType)
        ];
        Promise.all(promises).then(self.callback);
      },
      callback(data){
        const self = this;
        
        this.dialogData = data[0];

        this.addTextElements(this.dialogData);
      },
      addTextElements(data) {
        const self = this;

        let rects = this.svgGroup.selectAll("rect")
          .data(data)
          .enter()
          .append("rect")
            .attr("class", d => "rect " + d.class)
            .attr("x", 10)
            .attr("y", function(d,i) { return i*30 + 30 })
            .attr("height", 5)
            .attr("width", 5)
            .style("fill", "red")
            .on("click", (event, d) => self.populateCard(d)) //w/ d3v6 event is passed to listener as first parameter, datum as second

        let rectsText = this.svgGroup.selectAll("rectText")
          .data(data)
          .enter()
          .append("text")
            .attr("class", d => "rectText " + d.class)
            .attr("text-anchor", "start")
            .attr("x", 20)
            .attr("y", function(d,i) { return i*30 + 37 })
            .style("color", "red")
            .text(d => d.title)
            .on("click", (event, d) => self.populateCard(d)) //w/ d3v6 event is passed to listener as first parameter, datum as second
      },
      populateCard(d){
        const self = this;
        
        // Populate card with information
        this.cardHeader = d.header;
        this.cardTitle = d.title;
        this.cardText = d.text;
        let image_file = "@/assets/images/image_a.png"
        this.cardImageSource = require("@/assets/images/" + d.source);
        this.cardAltText = d.alt_text;
        this.showDialog = true;
      }
    },
} 
</script>

<style lang="scss">

</style>