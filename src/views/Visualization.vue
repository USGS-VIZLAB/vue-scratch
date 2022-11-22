<template>
  <div id="visualization">
    <authorship />
  </div>
</template>

<script>

export default {
    name: 'Visualization',
    components: {
      authorship: () => import( /* webpackPreload: true */ /*webpackChunkName: "section"*/ "./../components/Authorship")
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
