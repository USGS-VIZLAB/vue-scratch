<template>
  <section>

<div id="grid-container">
        <div id="rain-container">
            <!-- <svg id="rain-svg" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1600 900"></svg> -->   
        <canvas id="myCanvas" width="1600" height="900"></canvas>
        </div>
        <!--  <flowers /> -->
    </div>
  </section>
</template>
<script>
import * as d3Base from 'd3';
export default {
  name: "rain",
    components: {
        //flowers
    },
    data() {
    return {
      publicPath: process.env.BASE_URL, // this is need for the data files in the public folder, this allows the application to find the files when on different deployment roots


      // dimensions
      width: null,
      height: null,
      margin: { top: 50, right: 50, bottom: 50, left: 50 },
      svg: null,
      data_matrix: null,
      canvas: null,
      vueCanvas: null

 
    }
  },
  mounted(){
      this.d3 = Object.assign(d3Base);

      // resize
      this.width = window.innerWidth - this.margin.left - this.margin.right;
      this.height = window.innerHeight*.5 - this.margin.top - this.margin.bottom;

      this.canvas = document.getElementById('myCanvas')       
      this.makeItRain()

    },
    methods:{
     makeItRain() {
            // init canvas
      var ctx = this.canvas.getContext('2d');
      var w = this.canvas.width = window.innerWidth;
      var h = this.canvas.height = window.innerHeight;

      var yPositions = Array(60).join(0).split('');
      //var texty = this.getRandomInt(0,9);
      //console.log(texty)
    
    function runMatrix() {
    if (typeof Game_Interval != 'undefined') clearInterval(Game_interval);
           var Game_Interval = setInterval(drawScreen, 30); // higher = slower
        }

        function getRandomInt(min, max) {
         var min = Math.ceil(min);
         var max = Math.floor(max);
        return Math.floor(Math.random() * (max - min) + min);
    }

        function drawScreen () {
            ctx.fillStyle = 'rgba(255, 255, 255, .15)'; // higher a = shorter trails
            ctx.fillRect(0, 0, w, h);
            ctx.fillStyle = 'dodgerblue';
            ctx.font = '12px arial';
            yPositions.map(function(y, index){
            var text = "" + getRandomInt(0,2);
            //var text = String.fromCharCode(1e2 + Math.random() * 33);
            var x = (index * 20) + 20;
            ctx.fillText(text, x, y);
            if (y > 100 + Math.random() * 1e4) {
                yPositions[index] = 0;
            } else {
                yPositions[index] = y + 12; // how close together stacked vertically and dist travelled. 10 is ok

            }
            })
        }
        
        runMatrix();
     }
    }
}
</script>

<style scoped lang="scss">

body {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: flex-start;
}

 canvas {
    background-color: "white";
 }

</style>