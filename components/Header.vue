<template>
  <header class="header container">
    <h1 class="title">{{title}}</h1>
    <p class="infos">
      <!-- Itera sobre os generos do retorna da API --> 
      <span v-for="gen in genres" :key="gen.ID">
        {{gen.Title}} /
      </span>
      <span>{{year}}</span>
    </p>
  </header>
</template>

<script>
export default {
 
  props: {
    title: {
      type: String
    },
    year: {
      type: Number
    },
    genres: {
      type: Array
    }
  },

}
</script>

<style lang="scss">
  .header {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    z-index: $header;
    padding-top: 40px !important;
    > .title {
      font-size: 2.5rem;
      font-weight: normal;
      margin-bottom: 10px;
    }
    > .infos {
      font-size: 0.9rem;
      text-transform: uppercase;
      color: $text;
    }
    @include media('xs') {
      padding-top: 15px !important;
      > .title {
        font-size: 1.5rem;
        margin-bottom: 5px;
      }
    }
  }

</style>