<template>
  <div class="body">
    <principal-menu :routes="routes" />
    <transition name="pagina">
      <router-view></router-view>
    </transition>
  </div>
</template>

<script>
  import { routes } from './routes';
  import Menu from './components/shared/menu/Menu.vue';

  export default {
    components: {
      'principal-menu': Menu
    },

    data() {
      return {
        routes,
      }
    }  
  }
</script>

<style>
  .body {
    font-family: Helvetica, sans-serif;
    width: 96%;
    margin: 0 auto;
  }

  .pagina-enter-active, .pagina-leave-active {
    transition: opacity .3s
  }
  .pagina-enter, .pagina-leave-active {
    opacity: 0
  }
</style>
