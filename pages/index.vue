<template>
  <main>   
    <Header :title="tvshow.Title" :year="tvshow.Year" :genres="tvshow.Genres"/>
    <MenuButton :eventclick="handleOpen" />
    <div class="wrapper">
      <TabsEpisode :open="open" :episodes="episodes" />
      <Background :background="tvshow.Images.Background" :title="tvshow.Title" />
      <TabsMainInfos  :tvshow="tvshow" />
    </div>
  </main>
</template>

<script>
  import Background from '../components/Background.vue'
  import Header from '../components/Header.vue'
  import MenuButton from '../components/MenuButton.vue'
  import TabsEpisode from '../components/TabsEpisode.vue'
  import TabsMainInfos from '../components/TabsMainInfos.vue'

  export default {
    components: { TabsEpisode, Background, Header, TabsMainInfos, MenuButton },
    name: 'IndexPage',
    // Faz a requisição para a API e retorna as informações
    async asyncData({ $axios }) {
      const episodes = await $axios.$get('https://sample-api-78c77.firebaseio.com/episodes/SHOW123.json')
      const tvshow = await $axios.$get('https://sample-api-78c77.firebaseio.com/tv-shows/SHOW123.json')
      
      return { episodes, tvshow }
    },
    // Open serve para o clique do botão abrir a listagem de episodios
    // Por padrão vem fechado, ou seja, false
    data() {
      return {
        open: false,
      }
    },
    methods: {
      // Trata a abertura da listagem de episodios
      handleOpen(){
        this.open = !this.open

        // Adiciona classe auxiliar para trata o botão de menu da listagem: fechar e abrir
        this.$el.classList.toggle('openedlist')
      },
    }
  }
</script>

<style lang="scss">
  main {
    position: fixed;
    z-index: 3;
    left: 0;
    top: 0;
    width: 100%;
    &.openedlist {
      .menuopen {
        display: none;         
      }
      .close {
        display: block;
      }
    }
    .close {
      display: none;
    }
    @include media('xs') {
      .wrapper {
        height: 100%;
        position: relative;
      }
    }
  }
</style>