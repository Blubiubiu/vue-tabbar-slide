<template>
  <div id="app">
    <vue-tabbar-slide :options="options"></vue-tabbar-slide>
  </div>
</template>

<script>
import vueTabbarSlide from './lib/vueTabbarSlide'

export default {
  name: 'app',
  data () {
    return {
      options: {
        width: '50px'
      }
    }
  },
  components: {
    vueTabbarSlide
  }
}
</script>

<style lang="scss">
  * {
    margin: 0;
    padding: 0;
  }
</style>
