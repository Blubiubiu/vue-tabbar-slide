<template>
  <div id="app">
    <vue-tabbar-slide :options="options" @callback="callback"></vue-tabbar-slide>

    <div @click="getData">点击获取数据</div>
    <div @click="getData1">点击获取数据2</div>
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
    },
    getData1 () {
      this.options.slideData = ['data11', 'data21', 'data31', 'data41', 'data51', 'data61']
      console.log(this.options.slideData)
    },
    callback () {
      console.log('回调')
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
