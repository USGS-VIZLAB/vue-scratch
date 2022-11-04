<template>
  <div id='page-content'>
    <section>
      <button v-for="item in dialogData" :key="item.class" :id="item.class" class="itemButton" v-text="item.title" @click="textEvent"></button>
    </section>
    <section>
      <p>
        Here is some random text where we mention that there is an 
        <button id="item_a" class="itemButton" @click="textEvent">item A</button>
        and also an 
        <button id="item_b" class="itemButton" @click="textEvent">item B</button>
        , and 
        <button id="item_c" class="itemButton" @click="textEvent">item C</button>
        , and an 
        <button id="item_d" class="itemButton" @click="textEvent">item D</button>
        .
       </p>
    </section>
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
            self.d3.csv("https://labs.waterdata.usgs.gov/visualizations/data/dialog_data.csv", this.d3.autoType)
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
            .attr("class", d => "rect")
            .attr("id", d => d.class)
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
            .attr("class", d => "rectText")
            .attr("id", d => d.class)
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
        this.cardImageSource = "https://labs.waterdata.usgs.gov/visualizations/images/" + d.source;
        this.cardAltText = d.alt_text;
        this.showDialog = true;
      },
      textEvent(e) {
        const self = this;

        const item = e.target
        const itemID = item.id
        const itemData = self.getData(itemID)

        self.populateCard(itemData)
      },
      getData(itemID) {
        const self = this;

        let itemData = self.dialogData.filter(function(dataRow) {
          return dataRow.class === itemID
        })[0]

        return (itemData)
      }
    },
} 
</script>

<style lang="scss">
.itemButton {
  border-radius: 0.25rem;
  margin: 5px 0px 5px 5px;
  padding: 2.5px 5px 2.5px 5px;
  max-width: 24rem;
  background-color: white;
  border: 0.5px solid #949494;
  border-radius: 0.25rem;
  -webkit-user-select: none; /* Safari */
  -ms-user-select: none; /* IE 10 and IE 11 */
  user-select: none; /* Standard syntax */
}
.itemButton:hover {
  background-color: #949494;
  color: white;
  @media screen and (max-width: 600px) {
    background-color: white;
    color: black;
  }
}
</style>