<template>
  <Transition>
    <article class="tabside" v-if="handleReopened() == true">
      <div class="inner">
        <ul class="list">
          <li v-for="(temp, index) in filteredEpisodes" 
            :key="index" 
            :class="[ activeTabMenu == index ? 'active' : '' ]" 
          >
            <a href="javascript:void(0)" @click="activeTabMenu = index; activeTabPanelItem = null">
              T{{index}}
            </a>
          </li>
        </ul>

        <ul v-for="(temp, index) in filteredEpisodes" :key="index" class="tabpanel" >
          <template  v-if="activeTabMenu == index ">
            <li v-for="(episode, index) in temp" :key="index"  :title="'Duração ' + episode.Duration">
              <div class="wrapper">
                <a href="javascript:void(0)" :data-index="index"  @click="handleTabPanelItem">
                  {{index + 1}} {{ episode.Title }}
                </a>

                <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40">
                  <g fill="none" fill-rule="evenodd">
                      <circle cx="20" cy="20" r="19" stroke="#D8D8D8" stroke-width="2"/>
                      <path fill="#D8D8D8" d="M14.881 13.957v12.924a1 1 0 0 0 1.503.864l10.983-6.388a1 1 0 0 0 .008-1.724l-10.983-6.535a1 1 0 0 0-1.51.86z"/>
                  </g>
                </svg>
              </div>

              <div v-if="activeTabPanelItem == index" class="content">
                <figure class="imgcontainer">
                  <img :src="episode.Image" alt="placeholder">
                  <span class="progressbar">
                    <span class="progress"></span>
                  </span>
                </figure>
                <p class="description">
                  {{ episode.Synopsis }}
                </p>
              </div>
            </li>
          </template>
        </ul>

      </div>
    </article>
  </Transition>
</template>

<script>
  export default {
    data() {
      return {
        activeTabMenu: 1,
        activeTabPanelItem: null,
      }
    },
    props: {
      episodes: {
        type: Array,
        default() {return []}
      },
      open: {
        type: Boolean
      }
    },
    methods: {
      handleTabPanelItem(event){
        console.log('event', event.target.dataset.index);
        if (this.activeTabPanelItem == event.target.dataset.index) {
          this.activeTabPanelItem =  null
        } else {
          this.activeTabPanelItem = event.target.dataset.index
        }
      },
      handleReopened() {
        if (this.open == false) {
          this.activeTabPanelItem = null
        }

        return this.open
      }
    },
    computed: {
      filteredEpisodes() {
       const episodes = 
          this.episodes
          // Filtra limpando o objeto nulo
          .filter((value) => {  return value })
          // Reduz para separar os objetos por temporada
          .reduce((acumulador, ep) => { 
          if (!acumulador[ep.SeasonNumber]) {
            acumulador[ep.SeasonNumber] = []
          }
          acumulador[ep.SeasonNumber].push(ep)

          return acumulador
        }, {}) 

        // Retorna os objetos por temporada
        return episodes
      },
    }
  }
</script>

<style lang="scss">
  .v-enter-active,
  .v-leave-active {
    transition: transform 0.5s ease, opacity 0.5s ease;
  }
  .v-enter {
    transform: translate(100%);
  }
  .v-leave-to {
    transform: translate(100%);
  }
  .v-enter-from,
  .v-leave-to {
    opacity: 0;
  }
  .tabside {
    background: #00000050;
    width: 100%;
    max-width: 400px;
    height: 100%;
    position: absolute;
    right: 0;
    top: 0;
    padding-right: 3%;
    z-index: $tabEpisode;
    color: $text;
    @include media('xs') {
      backdrop-filter: blur(34px);
      background: transparent;
    }
    a {
      color: $text;
    }
    > .inner {
      padding-top: 60px;
      > .list {
        display: flex;
        align-content: center;
        justify-content: flex-start;
        border-bottom: 2px solid rgb(117, 117, 117);
      }
      > .list > li {
        height: 45px;
        display: flex;
        align-items: center;
        width: 41px;
        justify-content: center;
        cursor: pointer;
        &.active {
          position: relative;
          &:after {
            content: '';
            display: block;
            width: 100%;
            height: 2px;
            position: absolute;
            background-color: $bars;
            bottom: -2px;
            left: 0;
            border-radius: 2px;
          }
        }
      }
      > .tabpanel {
        padding: 0 5px;
        max-height: 50vh;
        overflow: auto;
        @include media('xs') {  
          max-height: 100%;
        }
      }
      > .tabpanel li {
        padding: 10px 0;
        display: flex;
        flex-direction: column;
        cursor: pointer;
        border-bottom: 1px solid $gray;
        user-select: none;
        > .wrapper {
          display: flex;
          align-items: center;
          justify-content: space-between;
          width: 100%;
          a {
            width: 100%;
            padding: 7px;
            display: block;
          }
        }
        svg {
          transition: transform 0.3s ease;
          &:hover {
            transform: scale(1.05);
          }
        }
      }
      .content {
        max-width: 90%;
        padding: 0 5px;
        figure {
          margin-bottom: 5px;
          display: flex;
          align-items: center;
          flex-direction: column;
        }
        img {
          width: 100%;
          height: auto;
          border-radius: 4px;
          display: block;
        }
      }
    }
  }
  .imgcontainer {
    position: relative;
    .progressbar {
      width: 100%;
      max-width: 90%;
      display: block;
      height: 3px;
      background: gray;
      position: absolute;
      bottom: 15px;
      z-index: $base;
      border-radius: 10px;

      .progress {
        width: 100%;
        display: block;
        background: $bars;
        height: 100%;
        width: 10%;
        border-radius: 10px;
      }
    }
  }
</style>