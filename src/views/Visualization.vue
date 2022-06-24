<template>
  <div id="visualization">
    <DragNDrop />
  </div>
</template>

<script>

export default {
    name: 'Visualization',
    components: {
      DragNDrop: () => import( /* webpackPreload: true */ /*webpackChunkName: "section"*/ "./../components/DragNDrop2")
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
