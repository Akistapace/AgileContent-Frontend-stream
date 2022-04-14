<template>
  <button type="button" ref="closebtn" class="menu" @click="eventclick">
    <svg class="close" xmlns="http://www.w3.org/2000/svg" width="28" height="27" viewBox="0 0 28 27">
      <g fill="none" fill-rule="evenodd" stroke="#FFF" stroke-linecap="round" stroke-width="2.5">
          <path d="M26.249 1.5L2.207 25.542M1.5 1.5l24.042 24.042"/>
      </g>
    </svg>

    <!-- Cria o menu hamburguer para abrir a listagem de episódios -->
    <div class="menuopen">
      <span class="bar -one"></span>
      <span class="bar -two"></span>
      <span class="bar -three"></span>
    </div>
  </button>
</template>

<script>
export default {
  props: {
    eventclick: {
      type: Function
    }
  }
}
</script>

<style lang="scss">
  .menu {
    position: absolute;
    right: 20px;
    top: 20px;
    background: transparent;
    border: none;
    cursor: pointer;
    z-index: 25;
    > .close {
      transition: transform 0.5s ease;
      &:hover {
        transform: rotate(180deg);
      }
    }
    > .menuopen {
      > .bar {
        display: block;
        height: 3px;
        width: 30px;
        background: #fff;
        position: relative;
        &.-one {
          display: block;
          height: 3px;
          width: 30px;
          background: #fff;
          top: -100%;
        }
        &.-two {
          margin-top: 5px;
          margin-bottom: 5px;
          transition: margin 0.2s linear;

        }
        &.-three {
          display: block;
          height: 3px;
          width: 30px;
          background: #fff;
          top: 100%;
        }
      }
      &:hover {
        > .bar.-two { 
          margin-top: 9px;
          margin-bottom: 9px;
        }        
      }
    }
  }
</style>