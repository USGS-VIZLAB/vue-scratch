<template>
  <div id="visualization">
    <ImageZoom />
  </div>
</template>

<script>

export default {
    name: 'Visualization',
    components: {
      ImageZoom: () => import( /* webpackPreload: true */ /*webpackChunkName: "section"*/ "./../components/ImageZoom")
    },
    computed: {
    },
    mounted(){
      
    },
    methods:{
    }
} 
</script>

<style lang="scss">

</style>
