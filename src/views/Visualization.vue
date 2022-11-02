<template>
  <div id="visualization">
    <useDialogCard />
  </div>
</template>

<script>

export default {
    name: 'Visualization',
    components: {
      useDialogCard: () => import( /* webpackPreload: true */ /*webpackChunkName: "section"*/ "./../components/UseDialogCard")
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
