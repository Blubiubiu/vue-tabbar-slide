<template>
  <div id="app">
    <vue-tabbar-slide :options="options" @callback="callback"></vue-tabbar-slide>
    <vue-tabbar-slide1 :options="options1" @callback="callback1"></vue-tabbar-slide1>

    <div @click="getData">点击获取数据</div>
    <div>第一行下标及数据{{callbackHtml}},<br>第二行下标及数据{{callbackHtml1}}</div>
  </div>
</template>

<script>
import vueTabbarSlide from './lib/vueTabbarSlide'

export default {
  name: 'app',
  data () {
    return {
      options: {
        container: 'mySlide1',
        slideData: [],
        slideId: [],
        width: '80px',
        index: 1
      },
      options1: {
        container: 'mySlide2',
        slideData: [],
        slideId: [],
        width: '80px',
        index: 1
      },
      callbackHtml: '',
      callbackHtml1: ''
    }
  },
  components: {
    vueTabbarSlide: vueTabbarSlide,
    vueTabbarSlide1: vueTabbarSlide
  },
  methods: {
    getData () {
      setTimeout(()=> {
        this.options.slideData = ['data1', 'data2', 'data3']
      this.options.slideId = ['1', '2', '3']
      }, 2000)
      this.options1.slideData = ['data11', 'data21', 'data31', 'data41', 'data51', 'data61']
      this.options1.slideId = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10']
    },
    callback (event, index, val, id) {
      this.callbackHtml = index + ';' + val + ';' + id
    },
    callback1 (event, index, val) {
      this.callbackHtml1 = index + ';' + val + ';' + id
    },
  }
}
</script>

<style lang="scss">
  * {
    margin: 0;
    padding: 0;
  }
</style>
