<template>
  <div v-show="show" class="overlay">


    <div class="dialog">
      <div class="dialog__header">
        <h3 class="dialog__header_text" v-text="header"></h3>
      </div>

      <hr class="dialog__break"/>

      <div class="dialog__content">
        <h2 class="dialog__title" v-text="title"></h2>
        <p class="dialog__text" v-text="text"></p>
        <div class="image__content">
          <img class="dialog__image" v-bind:src="source" width="200px" height="200px" v-bind:alt="altText">
        </div>
      </div>
    
      <hr class="dialog__break"/>

      <div class="dialog__footer">
        <button @click="close" class="button dialog__close"><p>Close</p></button>
      </div>

    </div>

  </div>
</template>

<script>
export default {
    props: ['show', 'header', 'title', 'text', 'source','altText', 'close']
}
</script>
<style>

.overlay {
  --tw-bg-opacity: 1;
  background-color: rgba(0, 0, 0, var(--tw-bg-opacity));
  --tw-bg-opacity: 0.5;
  height: 100%;
  position: fixed;
  top: 0px;
  right: 0px;
  bottom: 0px;
  left: 0px;
  width: 100%;
  z-index: 10;
}
.dialog {
  --tw-bg-opacity: 1;
  background-color: rgba(255, 255, 255, var(--tw-bg-opacity));
  border-radius: 0.75rem;
  overflow: hidden;
  margin-left: auto;
  margin-right: auto;
  margin-top: 2.5rem;
  width: 35rem;
  max-width: 90%;
  max-height: 90%;
}
.dialog__break {
  border: 0.5px solid black;
}
.dialog__header {
  -moz-border-radius: 0.75rem 0.75rem 0rem 0rem;
  padding-left: 0.75rem;
  padding-right: 0.75rem;
  padding-top: 0.25rem;
  padding-bottom: 0.25rem;
}
.dialog__content {
  padding-left: 0.75rem;
  padding-right: 0.75rem;
  padding-top: 1rem;
  padding-bottom: 1rem;
  height: 
}
.dialog__title {
  font-weight: 700;
  line-height: 1.75rem;
  margin-bottom: 0.5rem;
}
.dialog__header_text {
  font-weight: 500;
  line-height: 1.75rem;
  margin-bottom: 0.5rem;
}
.dialog__text {
  line-height: 1rem;
  font-weight: 500;
  padding: 0.25em 0 0 0;
}
.image__content {
  min-height: 200px;
}
.dialog__image {
  float: right;
  margin: 5px;
}
.dialog__footer {
  display: flex;
  justify-content: flex-end;
  padding-top: 0.05rem;
  padding-bottom: 0.05rem;
}
.dialog__close {
  border-radius: 0.75rem;
  font-weight: 400;
  margin-right: 1rem;
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  padding-left: 1rem;
  padding-right: 1rem;
  --tw-text-opacity: 1;
  color: #6E6E6E;
  -webkit-user-select: none;
     -moz-user-select: none;
      -ms-user-select: none;
          user-select: none;
}
.dialog__close:hover {
  --tw-text-opacity: 1;
  color: rgba(55, 65, 81, var(--tw-text-opacity));
  color: black;
  font-weight: 500;
}
</style>