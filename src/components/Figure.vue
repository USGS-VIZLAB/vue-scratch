<template>
  <div class="flex-container">
    <div class="flex-item">
      <source
          srcset=""
          type="image/webp"
          media="(max-width: 1200px)"
        >
      <picture>
        <source
          srcset=""
          type="image/jpg"
          media="(max-width: 1200px)"
        >
        <img
          v-img:group-1
          src=""
          alt=""
          loading="lazy"
        >
      </picture>
    </div>
  </div>
</template>

<script>
    export default {
        name: "Figure",
        props: {
            content: {
                type: String,
                required: true
            }
        },
        data() {
            return {

            }
        }
    }
</script>

<style scoped lang="scss">

</style>