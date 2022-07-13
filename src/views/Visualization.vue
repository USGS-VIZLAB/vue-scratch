<template>
  <div id="visualization">
    <Rain />
  </div>
</template>

<script>

export default {
    name: 'Visualization',
    components: {
      Rain: () => import( /* webpackPreload: true */ /*webpackChunkName: "section"*/ "./../components/rain")
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
