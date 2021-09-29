<template>
  <div id="visualization">
    <rain />
  </div>
</template>

<script>

export default {
    name: 'Visualization',
    components: {
      rain: () => import( /* webpackPreload: true */ /*webpackChunkName: "section"*/ "./../components/rain")
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
