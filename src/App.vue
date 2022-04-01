<template>
  <div id="app">
    <h1 class="text-danger text-uppercase m-4 shadow-lg" >boolflix</h1>
    <Main/>
  </div>
</template>

<script>
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Main
  }
}
</script>

<style lang="scss">
@import '@/style/main-style.scss';

</style>
