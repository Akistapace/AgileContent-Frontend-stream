<template>
  <section class="backgroundimg">
    <img :src="background" :alt="title">
  </section>
</template>

<script>
export default {
  props: {
    background: {
      type: String
    },
    title: {
      type: String
    }
  }
}
</script>

<style lang="scss">
  .backgroundimg {
    height: 100%;
    max-height: 100vh;
    width: 100%;
    overflow: hidden;
    position: relative;
    img {
      object-fit: cover;
      width: 100%;
      height: aut0;
    }
    &:after {
      position: absolute;
      content:"";
      height:100%;
      width:100%;
      bottom: 0;
      left:0;
      background: linear-gradient(to bottom, transparent 46%, rgba(0, 0, 0, 0.65) 65%,  rgba(0, 0, 0, 1) 90%)
    }
    &:before {
      position: absolute;
      content:"";
      height:100%;
      width:100%;
      top:0;
      left:0;
      background: linear-gradient(to top, transparent 46%, rgba(0, 0, 0, 0.65) 80%,  rgba(0, 0, 0, 1) 100%)
    }
  }
</style>