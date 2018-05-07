# vue-tabbar-slide

> A Vue.js Slide Tab-bar

<a href="https://www.npmjs.org/package/vue-tabbar-slide">
  <img src="https://img.shields.io/npm/v/vue-tabbar-slide.svg">
</a>

![image](https://github.com/Blubiubiu/vue-tabbar-slide/blob/master/gif/demo.gif)

## Install
```shell
npm install vue-tabbar-slide -S
```

## How To Use

``` javascript
//main.js
import Vue from 'vue'
import vueTabbarSlide from 'vue-tabbar-slide'

Vue.use(vueTabbarSlide)
```

``` vue
  <!-- app.vue -->
  <template>
    <div id="app">
      <vue-tabbar-slide :options="options" @callback="callback"></vue-tabbar-slide>

      <div @click="getData">点击获取数据</div>
      <div @click="getData1">点击更改数据</div>
    </app>
  </template>
```
``` javascript
  <script>
    export default {
      name: 'app',
      data () {
        return {
          options: {
            //required(必填项)
            container: 'mySlide1',
            slideData: [],
            //optional(可选项)
            width: '80px',
            index: 1
          },
        }
      },
      methods: {
        getData () {
          this.options.slideData = ['data1', 'data2', 'data3', 'data4', 'data5', 'data6', 'data7', 'data8', 'data9', 'data10']
        },
        getData1 () {
          this.options.slideData = ['data11', 'data21', 'data31', 'data41', 'data51', 'data61']
        },
        callback (event, index, val) {
          console.log(`callback=${index},${val}`)
        }
      }
    }
  </script>
```

## options

| Name | Type | Default | Description |
| ---- | ---- | ------- | ----------- |
| required |
| container | String | --- | container name |
| slideData | Array | --- | data |
| optional |
| slideIndex | Number | 0 | default index |
| width | String | 80px | slide width |
| height | String | 40px | slide height |
| textAlign | String | center | text-align |
| fontSize | String | 14px | font-size |
| fontFamily | String | Microsoft YaHei | font-family |
| color | String | #333 | font-color |
| checkedColor | String | #00a0e9 | checked-color |
| downLineHeight | String | 2px | underline height |
| downLineColor | String | #00a0e9 | underline color |

## Extension usage

![image](https://github.com/Blubiubiu/vue-tabbar-slide/blob/master/gif/demo.png)

you can use it to make a N-linkage and so on


#######
if you find some questions, please contact me!

bling_faker@163.com

if you like it, show me your star, thanks very much
