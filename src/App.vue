<template>
  <div id="app">
    <vue-tabbar-slide :options.sync="options"></vue-tabbar-slide>

    <div @click="getData">点击获取数据</div>
  </div>
</template>

<script>
import vueTabbarSlide from './lib/vueTabbarSlide'

export default {
  name: 'app',
  data () {
    return {
      options: {
        slideData: [],
        width: '80px'
      }
    }
  },
  components: {
    vueTabbarSlide
  },
  methods: {
    getData () {
      this.options.slideData = ['data1', 'data2', 'data3', 'data4', 'data5', 'data6', 'data7', 'data8', 'data9', 'data10']
      console.log(this.options.slideData)
    }
  }
}
</script>

<style lang="scss">
  * {
    margin: 0;
    padding: 0;
  }
</style>
