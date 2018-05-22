<template>
  <div class="tabbar-slide-wrapper">
    <div class="swiper-container" :class="options.container">
      <div class="swiper-wrapper">
        <div :style="[slideStyle, {'color': (index == slideOptions.slideIndex) ? slideStyle.checkedColor : slideStyle.color}]" :class="[index == slideOptions.slideIndex ? 'swiper-slide-checked' : '', 'swiper-slide']" v-for="(item, index) in options.slideData" :key="index" :data-id="slideOptions.slideId[index]">{{item}}</div>
        <!-- 下划线 -->
        <div :style="{width: slideStyle.width, height: downLineStyle.downLineHeight, background: downLineStyle.downLineColor}" ref="slideDownLine" class="slide-down-line"></div>
      </div>
    </div>
    <div class="tabbar-slide-container"></div>
  </div>
</template>

<script>
  import Swiper from 'swiper'
  import '../../node_modules/swiper/dist/css/swiper.min.css'

  export default {
    name: 'vueTabbarSlide',
    props: ['options', 'slideId'],
    data () {
      return {
        mySwiper: null,
        //数据
        slideArr: this.options.slideData || ['slide1', 'slide2', 'slide3', 'slide4', 'slide5', 'slide6', 'slide7', 'slide8', 'slide9', 'slide10', 'slide11', 'slide12', 'slide13'],
        //样式
        slideStyle: {
          //宽度
          width: this.options.width || '80px',
          //高度
          height: this.options.height || '40px',
          //垂直高度
          lineHeight: this.options.height || '40px',
          //文本排列方式
          textAlign: this.options.textAlign || 'center',
          //字体大小
          fontSize: this.options.fontSize || '14px',
          //字体格式
          fontFamily: this.options.fontFamily || 'Microsoft YaHei',
          //默认字体颜色
          color: this.options.color || '#333',
          //选中字体颜色
          checkedColor: this.options.checkedColor || '#00a0e9'
        },
        downLineStyle: {
           //下划线高度
          downLineHeight: this.options.downLineHeight || '2px',
          //下划线颜色
          downLineColor: this.options.downLineColor || '#00a0e9',
        },
        //选项
        slideOptions: {
          slideIndex: this.options.index || 0
        },
        //下划线
        slideDownLine: null
      }
    },
    watch: {
      options: {
        //此处不要用箭头函数，this会跑偏 ^_^
        handler: function(newValue, oldValue) {
          if (this.mySwiper) {
            this.mySwiper.destroy(true, false)
          }
          this.mySwiper = new Swiper(`.${this.options.container}`, {
            slidesPerView: "auto",
            freeMode: true,
            freeModeMomentumRatio: 0.5,
            observer: true,
            observeParents: false,
            on: {
              init: () => {
                //默认选中
                this.slideOptions.slideIndex = this.options.index || 0
                //下划线
                this.$refs.slideDownLine.style.transform = `translateX(${this.slideOptions.slideIndex*parseInt(this.slideStyle.width)}px)`
                //回调函数
                this.$emit("callback", event, this.slideOptions.slideIndex, this.options.slideData[this.slideOptions.slideIndex])
              },
              tap: () => {
                //滑动时间
                this.mySwiper.setTransition(300)
                //滑动
                this.slide(swiperWidth, maxTranslate, maxWidth)
                //更改class
                this.slideOptions.slideIndex = this.mySwiper.clickedIndex
                //下划线
                this.$refs.slideDownLine.style.transform = `translateX(${this.slideOptions.slideIndex*parseInt(this.slideStyle.width)}px)`
                //回调函数
                this.$emit("callback", event, this.mySwiper.clickedIndex, event.target.innerText)
              }
            }
          });
          //swiper可视宽度
          const swiperWidth = this.mySwiper.width
          //swiper最大移动距离
          const maxTranslate = swiperWidth - (parseInt(this.options.width) * this.options.slideData.length)
          //
          const maxWidth = -maxTranslate + swiperWidth / 2
  　　　},
  　　　deep: true
      }
    },
    methods: {
      slide(swiperWidth, maxTranslate, maxWidth) {
        //点击的slide
        const slide = this.mySwiper.slides[this.mySwiper.clickedIndex]
        //点击的slide offsetLeft距离浏览器左边距离
        const slideLeft = slide.offsetLeft
        //点击的slide的可视宽度
        const slideWidth = slide.clientWidth
        // 被点击slide的中心点
        const slideCenter = slideLeft + slideWidth / 2
        //当中心点距离少于一半宽度时
        if (slideCenter < swiperWidth / 2) {

          this.mySwiper.setTranslate(0)

        } else if (slideCenter > maxWidth) {

          this.mySwiper.setTranslate(maxTranslate)

        } else {

          const nowTlanslate = slideCenter - swiperWidth / 2

          this.mySwiper.setTranslate(-nowTlanslate)

        }
        //选中颜色
        slide.style.color = this.downLineStyle.downLineColor
      }
    }
  }
</script>

<style>

  .tabbar-slide-wrapper {
    width: 100%;
    background: #fff;
  }
  .swiper-slide {
    word-break: keep-all;
    overflow: hidden;
  }
  .slide-down-line {
    position: absolute;
    left: 0;
    bottom: 0;
    transition: transform .3s;
    transform: translateX(0);
  }
</style>
