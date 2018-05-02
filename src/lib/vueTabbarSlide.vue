<template>
  <div class="tabbar-slide-wrapper">
    <div class="tabbar-slide">
      <div :style="slideOptions" class="tabbar-slide-list" ref="slide" v-for="(item, index) in slideArr" :key="index">
        {{item}}
      </div>
    </div>
    <div class="tabbar-slide-container"></div>
  </div>
</template>

<script>
  export default {
    name: 'vueTabbarSlide',
    props: ['options'],
    data () {
      return {
        slideArr: [1,2,3,4,5,6,7,8,9,10],
        slideOptions: {
          flex: `0 0 ${this.options.width}` || '0 0 50px'
        }
      }
    },
    mounted () {

    }
  }
</script>

<style>
  .tabbar-slide-wrapper {
    width: 100%;
    background: #eee;
    border-bottom: 1px solid red;
    overflow: hidden;
    font-family: 'Microsoft YaHei';
    font-size: 14px;
  }
  .tabbar-slide {
    display: flex;
    align-items: center;
  }
  .tabbar-slide-list {
    background: red;
  }
</style>
