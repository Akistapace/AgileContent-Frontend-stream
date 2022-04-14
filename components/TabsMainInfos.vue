<template>
  <section class="tabsMain">
    <ul class="tabitemmain">
      <!-- {{tvshow}} -->
      <li data-index="1" @click="handleClick" :class="[ tabMainActive == 1 ? 'active' : '' ]" >
        General
      </li>
      <li data-index="2" @click="handleClick" :class="[ tabMainActive == 2 ? 'active' : '' ]" >
        Elenco
      </li>
      <!-- <li data-index="3" @click="handleClick" :class="[ tabMainActive == 3 ? 'active' : '' ]" >Principais Premios</li> -->
      
      <!-- Icone do telecine -->
      <li class="icontelecine" title="Telecine">
        <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="49" height="30" viewBox="0 0 49 30">
          <defs><path id="a" d="M0 .417h47.959v27.747H0z"/></defs>
          <g fill="none" fill-rule="evenodd">
            <g transform="translate(.376 1.834)">
              <mask id="b" fill="#fff"><use xlink:href="#a"/></mask>
              <path fill="#FFF" d="M19.85 15.375h-.138c-1.028 0-2.055.002-3.082-.004-.129 0-.15.04-.15.149.003 2.964.003 5.927 0 8.89 0 .117.034.146.154.145 1.02-.004 2.04-.002 3.059-.002.157 0 .157 0 .157-.147v-9.031zm-9.923 5.667c-.15.135-.278.266-.422.379-.47.366-1.003.554-1.612.434-1.329-.26-2.092-1.795-1.235-2.945a1.88 1.88 0 0 1 1.54-.787c.502-.01.942.175 1.333.465.135.1.26.212.394.324l2.65-1.709c-1.486-1.863-3.723-2.688-6.034-1.918-1.89.63-3.828 2.521-3.496 5.167.22 1.753 1.439 3.906 4.208 4.413a5.31 5.31 0 0 0 5.26-2.082l-2.586-1.741zM37.38 15.42v.137l-.001 1.605-.015 7.24c0 .088-.01.157.13.157 2.392-.005 4.783-.004 7.175-.002.107 0 .135-.03.135-.129-.005-.626-.002-1.252-.002-1.878v-.132h-4.094v-1.256H44.6c.173 0 .173 0 .173-.168v-1.97c0-.156 0-.156-.163-.156H40.71v-1.35h4.045V15.42H37.38zm-13.447-.339c-.005.064-.01.1-.01.136 0 3.059 0 6.118-.002 9.176 0 .103.033.127.137.127.923-.004 1.847-.002 2.77-.003.04 0 .077-.004.13-.007v-3.553l6.177 3.961V15.4H33c-.876 0-1.751.002-2.627-.003-.118 0-.145.034-.145.141.004 1.108.003 2.216.003 3.324v.144l-6.297-3.925zM0 16.607v-4.144l.12.003 11.29.014 6.755.006 13.005.013c2.228.003 4.455.007 6.683.009l9.97.007h.136v15.648h-.15l-2.795-.003-5.626-.006-8.447-.004c-6.451-.002-12.902-.002-19.353-.005-3.795-.001-7.59-.005-11.386-.008-.17 0-.17 0-.17-.158L.014 16.787c0-.06-.01-.12-.014-.18z" mask="url(#b)"/>
            </g>
            <path fill="#FFF" d="M23.241.436v2.25h-4.235v1.48h4.248v2.43h-4.253v1.369h4.28v2.267h-7.834V.436zM14.038.436v2.578h-2.78v7.218h-3.45v-7.21h-2.91V.436zM36.545 10.232V.436h7.8v2.243h-4.291v1.463h4.299v2.442h-4.296V7.97h4.323v2.262zM29.124 7.612h3.401v2.62h-6.529V.436h3.128z"/>
          </g>
        </svg>
      </li>
    </ul>

    <div class="general" v-if="tabMainActive == 1">
      <ul class="listicons">
        <li @click="handleAddFavorite" class="favoritelist">
          <svg xmlns="http://www.w3.org/2000/svg" width="34" height="34" viewBox="0 0 34 34">
            <g fill="none" fill-rule="evenodd" stroke="#9B9B9B">
              <path fill-rule="nonzero" stroke-width="1.5" d="M17 33c8.822 0 16-7.177 16-16 0-8.822-7.178-16-16-16S1 8.177 1 17c0 8.822 7.178 16 16 16z"/>
              <g transform="translate(10 10)">
                  <rect width="1" height="13" x="6.5" y=".5" rx=".5"/>
                  <rect width="1" height="13" x="6.5" y=".5" rx=".5" transform="rotate(90 7 7)"/>
              </g>
            </g>
          </svg>
          <small v-show="favorite == false">Minha Lista</small>
          <small v-show="favorite == true">Adicionado</small>
        </li>
       
        <li @click="handleRate" class="rate">
          <svg v-show="rate == false" class="rate-negative" xmlns="http://www.w3.org/2000/svg" width="34" height="34" viewBox="0 0 34 34">
              <g fill="none" fill-rule="evenodd" transform="translate(1 1)">
                  <path stroke="#9B9B9B" stroke-width="1.5" d="M16 32c8.822 0 16-7.177 16-16 0-8.822-7.178-16-16-16S0 7.177 0 16c0 8.822 7.178 16 16 16z"/>
                  <path fill="#9B9B9B" fill-rule="nonzero" d="M16.237 19.556a7.548 7.548 0 0 1 6.257 3.329 1.178 1.178 0 1 1-1.952 1.32 5.194 5.194 0 0 0-4.305-2.294 5.195 5.195 0 0 0-4.305 2.293 1.178 1.178 0 0 1-1.952-1.32 7.548 7.548 0 0 1 6.257-3.328z"/>
                  <circle cx="7.111" cy="14.222" r="1.778" fill="#9B9B9B"/>
                  <circle cx="24.889" cy="14.222" r="1.778" fill="#9B9B9B"/>
              </g>
          </svg>

          <svg v-show="rate == true" :class="[ rate == true ? 'active' : '' ]" class="rate-positive" width="34" height="34" xmlns="http://www.w3.org/2000/svg">
            <g>
              <title>Layer 1</title>
              <g id="svg_1" fill-rule="evenodd" fill="none">
              <path id="svg_2" d="m17,33c8.822,0 16,-7.177 16,-16c0,-8.822 -7.178,-16 -16,-16s-16,7.177 -16,16c0,8.822 7.178,16 16,16z" stroke-width="1.5" stroke="#9B9B9B"/>
              <path transform="rotate(180 17.2373 23.14)" id="svg_3" d="m17.237,20.556a7.548,7.548 0 0 1 6.257,3.329a1.178,1.178 0 1 1 -1.952,1.32a5.194,5.194 0 0 0 -4.305,-2.294a5.195,5.195 0 0 0 -4.305,2.293a1.178,1.178 0 0 1 -1.952,-1.32a7.548,7.548 0 0 1 6.257,-3.328z" fill-rule="nonzero" fill="#9B9B9B"/>
              <circle id="svg_4" fill="#9B9B9B" r="1.778" cy="15.222" cx="8.111"/>
              <circle id="svg_5" fill="#9B9B9B" r="1.778" cy="15.222" cx="25.889"/>
              </g>
            </g>
          </svg>

          <small v-show="rate == false">Avaliar</small>
          <small v-show="rate == true">Obrigado!</small>
        </li>

        <li>
          <svg class="record" xmlns="http://www.w3.org/2000/svg" width="34" height="34" viewBox="0 0 34 34">
              <g fill="none" fill-rule="evenodd" transform="translate(1 1)">
                  <path stroke="#9B9B9B" stroke-width="1.5" d="M16 32c8.822 0 16-7.177 16-16 0-8.822-7.178-16-16-16S0 7.177 0 16c0 8.822 7.178 16 16 16z"/>
                  <circle cx="16.143" cy="16.143" r="3.699" fill="#9B9B9B"/>
              </g>
          </svg>
           <small>Gravar</small>
        </li>

        <li class="share">
          <svg xmlns="http://www.w3.org/2000/svg" width="34" height="34" viewBox="0 0 34 34">
            <g fill="none" fill-rule="nonzero">
              <path stroke="#9B9B9B" stroke-width="1.5" d="M17 33c8.822 0 16-7.177 16-16 0-8.822-7.178-16-16-16S1 8.177 1 17c0 8.822 7.178 16 16 16z"/>
              <path class="arrow" fill="#9B9B9B" d="M15.186 10.943l1.144-1.147v9.096c0 .49.396.887.884.887a.886.886 0 0 0 .884-.887V9.796l1.144 1.147a.88.88 0 0 0 1.25 0 .89.89 0 0 0 0-1.255L17.84 7.027a.903.903 0 0 0-.066-.06l-.03-.022-.04-.029-.037-.023-.036-.022c-.013-.007-.026-.012-.04-.018-.012-.007-.025-.013-.039-.019l-.038-.014-.044-.015-.038-.01-.045-.011-.045-.007-.04-.006a.902.902 0 0 0-.083-.004h-.01a.884.884 0 0 0-.082.004c-.014.001-.027.004-.04.006l-.046.007-.044.01-.04.01-.042.016-.04.014-.037.018c-.014.006-.028.012-.041.02l-.035.02-.04.024-.036.028-.033.024a.896.896 0 0 0-.062.056l-.003.002-2.653 2.662a.89.89 0 0 0 0 1.255.883.883 0 0 0 1.251 0z"/>
              <path fill="#9B9B9B" d="M22.959 13H20.66a.863.863 0 0 0-.862.864c0 .478.386.865.862.865h1.436v8.644H12.33V14.73h1.436a.863.863 0 0 0 .862-.865.863.863 0 0 0-.862-.864H11.47a.863.863 0 0 0-.862.864v10.374c0 .477.386.864.862.864h11.489a.863.863 0 0 0 .861-.864V13.864A.863.863 0 0 0 22.96 13z"/>
            </g>
          </svg>
          <small>Compartilhar</small>
        </li>
       
      </ul>

      <div class="sinopsis">
        <h3 class="title">Sinopse</h3>
        <p class="description">{{tvshow.Synopsis}}</p>
      </div>
    </div>

    <div class="cast" v-if="tabMainActive == 2">
       <SliderCast
        :update="tabMainActive"
        :cast="tvshow.Cast"
        />
    </div>

    <div class="principals" v-show="tabMainActive == 3">

    </div>
    
  </section>
</template>

<script>

export default {
  data() {
    return {
      tabMainActive: 1,
      rate: false,
      favorite: false
    }
  },
  props: {
    tvshow: {
      type: Object
    }
  },
  methods: {
    handleClick(event) {
      this.tabMainActive = event.target.dataset.index
    },
    handleRate() {
      this.rate = !this.rate
    },
    handleAddFavorite() {
      this.favorite = !this.favorite
    }
  }
}
</script>

<style lang="scss">
  .tabsMain {
    padding: 20px 5% 10px 5%;
    position: absolute;
    bottom: 0;
    background: #2a2a2a;
    width: 100%;
    z-index: $tabMain;
    min-height: 190px;
    @include media('xs') {
     position: initial;
    }
  }
  .tabitemmain {
    position: relative;
    display: flex;
     &:after {
      content: '';
      display: block;
      height: 2px;
      width: 100%;
      background: $gray;
      position: absolute;
      left: 0;
      bottom: -10px;
      border-radius: 30px;
    } 
    li {
      text-transform: uppercase;
      margin-right: 45px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      h2 {
        font-weight: 400;
      }
      &.active {
        position: relative;
        &:after {
          content: '';
          display: block;
          height: 2px;
          width: 100%;
          background: $bars;
          position: absolute;
          left: 0;
          bottom: -10px;
          z-index: 1;
          border-radius: 30px;
        } 
      }
      &.icontelecine {
        margin-left: auto;
        margin-right: 0;
      }
    }
  }
  .general {
    display: flex;
    gap: 30px;
    padding-top: 40px;
    @include media('xs') {
      flex-direction: column;
    }
    svg {
      transition: transform 0.3s ease;
      &:hover {
        transform: scale(1.05);
      }
    }
    > .listicons {
      display: flex;
      justify-content: space-between;
      flex: 1;
      li {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        cursor: pointer;
        min-width: 70px;
        &:not(:last-child) {
          margin-right: 10px;
        }
        svg {
          margin-bottom: 7px;
        }
      }
      .favoritelist {
        g > g rect {
          transition: stroke 0.3s linear;
        }
        &:hover {
          g > g rect {
            stroke: $bars;
          }
        }
      }
      .rate {
        .rate-negative *,
        .rate-positive * {
          transition: all 0.3s linear;
        }
        .rate-positive.active {
          circle{
            fill: $bars;
          }
          path:first-child {
            stroke: $bars;
          }
          path:nth-child(2) {
            fill: $bars;
          }
        }

        &:hover {
          .rate-negative {
            circle{
              fill: #be0000;
            }
            path:first-child {
              stroke: #be0000;
            }
            path:nth-child(2) {
              fill: #be0000;
            }
          }
          .rate-positive {
            &:hover {
              circle{
                fill: $bars;
              }
              path:first-child {
                stroke: $bars;
              }
              path:nth-child(2) {
                fill: $bars;
              }
            }
          }
        }
      }
      .record {
        circle {
          transition: fill 0.3s linear;
        }
        &:hover circle {
          fill: red;
        }
      }
      .share {
        .arrow {
          transition: transform 0.3s linear;
        }
        &:hover {
          .arrow {
            transform: translateY(-4px);
          }
        }
      }
    }
    > .sinopsis {
      flex: 2.5;
      color: $text;
      > .title {
        text-transform: uppercase;
        font-weight: 400;
      }
    }
  }
  .cast {
    padding-top: 40px;
  }

</style>