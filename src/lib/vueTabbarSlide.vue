<template>
  <div class="tabbar-slide-wrapper">
    <!-- <div class="tabbar-slide">
      <div :style="slideOptions" class="tabbar-slide-list" ref="slide" v-for="(item, index) in slideArr" :key="index">
        {{item}}
      </div>
    </div> -->
    <div class="swiper-container">
      <div class="swiper-wrapper">
        <div :style="slideStyle" :class="[index == slideOptions.slideIndex ? 'swiper-slide-checked' : '', 'swiper-slide']" ref="slide" v-for="(item, index) in slideArr" :key="index">{{item}}</div>
        <div ref="slideDownLine" class="slide-down-line"></div>
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
    props: ['options'],
    data () {
      return {
        mySwiper: null,
        //数据
        slideArr: [1,2,3,4,5,6,7,8,9,10],
        //样式
        slideStyle: {
          //宽度
          width: this.options.width || '50px',
          //文本排列方式
          textAlign: this.options.textAlign || 'center',
          //字体大小
          fontSize: this.options.fontSize || '14px',
          //字体格式
          fontFamily: this.options.fontFamily || 'Microsoft YaHei'.mySwiper
        },
        //选项
        slideOptions: {
          slideIndex: 0
        },
        //下划线
        slideDownLine: null
      }
    },
    mounted () {
      this.mySwiper = new Swiper('.swiper-container', {
        slidesPerView: "auto",
        freeMode: true,
        freeModeMomentumRatio: 0.5,
        on: {
          tap: () => {
            //滑动时间
            this.mySwiper.setTransition(300)
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
            //更改class
            this.slideOptions.slideIndex = this.mySwiper.clickedIndex
            //下划线
            this.$refs.slideDownLine.style.transform = `translateX(${this.slideOptions.slideIndex*50}px)`
          }
        }
      });

      //swiper可视宽度
      const swiperWidth = this.mySwiper.width
      //swiper最大移动距离
      const maxTranslate = this.mySwiper.maxTranslate()
      //
      const maxWidth = -maxTranslate + swiperWidth / 2


    },
    methods: {

    }
  }
</script>

<style>

  .tabbar-slide-wrapper {
    width: 100%;
    background: #fff;
  }
  .swiper-wrapper {

  }
  .swiper-slide {

  }
  .swiper-slide-checked {
    color: blueviolet;
  }
  .slide-down-line {
    position: absolute;
    width: 50px;
    height: 1px;
    left: 0;
    bottom: 0;
    background: red;
    transition: transform .3s;
    transform: translateX(0);
  }
</style>
