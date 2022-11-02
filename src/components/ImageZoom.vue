<template>
  <section>
    <div id="content-container">
      <div
        id="button-container"
        class="buttonContainer"
      >
        <h3>
          <span>
            Zoom:
            <button
              class="zoom button"
              @click="$refs.zoomer.zoomIn()"
            > + </button>
            <button
              class="zoom button"
              @click="$refs.zoomer.zoomOut()"
            > - </button>
          </span> 
        </h3>
      </div>
      <v-zoomer
        id="image-zoomer"
        ref="zoomer"
        :aspect-ratio="imageAspectRatio"
        :max-scale="10"
        :zooming-elastic="false"
        class="content"
      >
        <picture>
          <source
            :srcset="imageSrcWebp"
            type="image/webp"
          >
          <source
            :srcset="imageSrc"
            type="image/png"
          >
          <img
            :src="imageSrcWebp"
            style="object-fit: contain; width: 100%; height: 100%; display: flex;"
            @load="onImageLoad"
          >
        </picture>
      </v-zoomer>
    </div>
  </section>
</template>
<script>
export default {
  name: "ImageZoom",
    components: {
        //flowers
    },
    data() {
    return {
      zoomed: false,
      imageAspectRatio: 1,
      imageSrc: null,
      imageSrcWebp: null
    }
  },
  mounted(){
      this.imageSrc = "https://labs.waterdata.usgs.gov/visualizations/images/USGS_WaterCycle_English_ONLINE.png";
      this.imageSrcWebp = "https://labs.waterdata.usgs.gov/visualizations/images/USGS_WaterCycle_English_ONLINE.png";

    },
    methods:{
      onImageLoad(e) {
            const img = e.target
            this.imageAspectRatio = img.naturalWidth / img.naturalHeight
          },
    }
}
</script>

<style scoped lang="scss">

#image-zoomer {
  height: 85vh;
}
#button-container {
  padding-left: 15px;
  height: 100%;
  z-index: 2;
  --tw-bg-opacity: 1;
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
    -khtml-user-select: none; /* Konqueror HTML */
      -moz-user-select: none; /* Old versions of Firefox */
      -ms-user-select: none; /* Internet Explorer/Edge */
          user-select: none; /* Non-prefixed version, currently
                                supported by Chrome, Edge, Opera and Firefox */
}
.button {
  border-radius: 0.25rem;
  margin-right: 2px;
  margin-top: 2px;
  padding: 2.5px 5px 2.5px 5px;
  max-width: 24rem;
  background-color: white;
  border: 0.5px solid #949494;
  border-radius: 0.25rem;
  margin-left: 0.5rem;
  margin-top: 0.5rem;
  -webkit-user-select: none; /* Safari */
  -ms-user-select: none; /* IE 10 and IE 11 */
  user-select: none; /* Standard syntax */
}
.button:hover {
  background-color: #6E6E6E;
  color: white;
  @media screen and (max-width: 600px) {
    background-color: white;
    color: black;
  }
}
.button.zoom {
  padding: 2.5px 10px 2.5px 10px;
}
</style>