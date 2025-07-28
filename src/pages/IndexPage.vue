<template>
  <q-page class="flex flex-center" style="height: 1px">
    <swiper
      :style="{
        '--swiper-navigation-color': '#fff',
        '--swiper-pagination-color': '#fff',
      }"
      :speed="600"
      :slidesPerView="'auto'"
      :parallax="true"
      :freeMode="true"
      :mousewheel="true"
      :modules="modules"
      class="mySwiper"
      @slideChange="onSlideChange"
      @progress="onProgress"
      ref="swiperInstance"
    >
      <div
        slot="container-start"
        class="parallax-bg"
        :style="{
          'background-image':
            'url(https://rprojectjapan.com/assets/images/top/exhibition/bg_1_blur.webp)',
        }"
        data-swiper-parallax="-23%"
      ></div>
      <swiper-slide id="slide1">
        <h1 style="font-family: 'Kosugi Maru', sans-serif">歡迎光臨</h1>
        <h3 class="q-ma-none">Bob的最後模板作業</h3>
      </swiper-slide>
      <swiper-slide>
        <!-- <q-btn id="btn1" @click="handleClick" color="amber" glossy label="Amber" /> -->
        <div class="card" @mouseenter="onCardHover" @mouseleave="onCardLeave">
          <img src="https://rprojectjapan.com/assets/images/top/exhibition/story_image_1.webp" />
          <div ref="title1" class="title" data-swiper-parallax="100%">STORY</div>
          <div class="subtitle" data-swiper-parallax="-300">01</div>
        </div>
      </swiper-slide>
      <swiper-slide>
        <div class="card">
          <img src="https://rprojectjapan.com/assets/images/top/exhibition/story_image_2.webp" />
          <div ref="title2" class="title" data-swiper-parallax="0">STORY</div>
          <div class="subtitle" data-swiper-parallax="-300">02</div>
        </div>
      </swiper-slide>
      <swiper-slide>
        <div class="card">
          <img src="https://rprojectjapan.com/assets/images/top/exhibition/story_image_3.webp" />
          <div class="title" data-swiper-parallax="-200">STORY</div>
          <div class="subtitle" data-swiper-parallax="-300">03</div>
        </div>
      </swiper-slide>
      <swiper-slide>
        <div class="card">
          <img src="https://rprojectjapan.com/assets/images/top/exhibition/story_image_4.webp" />
          <div class="title" data-swiper-parallax="-300">STORY</div>
          <div class="subtitle" data-swiper-parallax="-300">04</div>
        </div>
      </swiper-slide>
    </swiper>
  </q-page>
</template>

<script setup>
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from 'swiper/vue'

// Import Swiper styles
import 'swiper/css'

import 'swiper/css/pagination'
import 'swiper/css/navigation'
import 'swiper/css/free-mode'

// import required modules
import { Parallax, FreeMode, Mousewheel } from 'swiper/modules'

// gsap
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

// animejs
import { animate, stagger, text } from 'animejs'

const modules = [Parallax, FreeMode, Mousewheel]

gsap.registerPlugin(ScrollTrigger)

const subtitles = ref([])

const onCardHover = (event) => {
  const card = event.currentTarget
  const img = card.querySelector('img')

  // 放大
  gsap.to(img, {
    scale: 1.2,
    duration: 0.5,
    ease: 'power1.out',
  })
}

const onCardLeave = (event) => {
  const card = event.currentTarget
  const img = card.querySelector('img')

  // 恢復圖片大小
  gsap.to(img, {
    scale: 1,
    duration: 0.5,
    ease: 'power1.out',
  })
}

// const handleClick = () => {
//   if (title1.value) {
//     // 點擊按鈕後，為 title1 元素設置動畫
//     console.log('click')
//     gsap.to(title1.value, {
//       x: 100, // 水平移動 100px
//       duration: 1, // 動畫持續 1 秒
//       ease: 'power1.out', // 平滑過渡效果
//     })
//   }
// }

//
const onSlideChange = (swiper) => {
  console.log('Slide:', swiper.activeIndex)

  // if (swiper.activeIndex < 2) return

  // if (subtitles.value[swiper.activeIndex - 2]) {
  //   console.log(
  //     'Slide changed to:',
  //     swiper.activeIndex,
  //     subtitles.value[swiper.activeIndex - 2].textContent,
  //   )
  //   gsap.to(subtitles.value[swiper.activeIndex - 2], {
  //     x: 400,
  //     duration: 5,
  //     ease: 'power1.inOut',
  //   })
  // } else {
  //   console.warn('Subtitle not found for slide index:', swiper.activeIndex - 2)
  // }

  // 當滑動到第3張（index為2）時觸發 title2 動畫
  // if (swiper.activeIndex === 2 && title2.value) {
  //   console.log(' -- 觸發 title2 動畫 --')
  //   gsap.to(title2.value, {
  //     x: 400,
  //     duration: 5,
  //     ease: 'power1.inOut',
  //   })
  // }
}

const onProgress = (swiper, progress) => {
  //console.log('Slide:', swiper.activeIndex)
  // console.log('Swiper progress:', progress)
  // 根據滑動進度觸發動畫
  // if (progress > 0.4 && title2.value) {
  //   console.log(' -- 觸發 title2 動畫 --', progress)
  //   gsap.to(title2.value, {
  //     x: progress * 500, // 根據滑動進度調整動畫
  //     duration: 0.3,
  //     ease: 'power1.out',
  //   })
  // }
}

onMounted(() => {
  //
  subtitles.value = Array.from(document.querySelectorAll('.subtitle'))

  // 開頭
  const { chars } = text.split('#slide1 h1', { words: false, chars: true })

  if (chars && chars.length > 0) {
    animate(chars, {
      y: [
        { to: '-5rem', ease: 'outExpo', duration: 1000 },
        { to: 0, ease: 'outBounce', duration: 800, delay: 100 },
      ],
      rotate: {
        from: '-1turn',
        delay: 0,
      },
      delay: stagger(200),
      ease: 'inOutCirc',
      loopDelay: 2000,
      loop: false,
    })
  }
})

// onMounted(() => {
//   if (title2.value) {
//     // 為該元素設置滾動動畫
//     gsap.to(title2.value, {
//       // x: () => Math.random() * 20 - 10, // 隨機水平抖動 (-10 到 10px)
//       // y: () => Math.random() * 20 - 10, // 隨機垂直抖動 (-10 到 10px)
//       x: 500,
//       duration: 100, // 每次抖動的持續時間
//       // repeat: -1, // 無限重複
//       ease: 'power1.inOut', // 平滑的動畫效果
//       scrollTrigger: {
//         trigger: title2.value, // 滾動觸發的目標
//         start: 'left center',
//         end: 'right left',
//         scrub: true, // 滾動時同步動畫
//         markers: true,
//         scroller: '.mySwiper', // 指定水平滾動容器
//         horizontal: true, // 啟用水平觸發
//         onEnter: () => console.log('ScrollTrigger: Entered'),
//         onLeave: () => console.log('ScrollTrigger: Left'),
//         onUpdate: (self) => console.log('ScrollTrigger: Progress', self.progress),
//       },
//     })
//   }
// })
</script>

<style scoped>
#slide1 {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%; /* 確保占滿父容器高度 */
}

.swiper {
  width: 100%;
  height: 100%;
  background: #000;
  border: 5px solid blue;
}

.swiper-slide:nth-child(2n + 2) .card {
  border: 5px solid cyan;

  position: absolute;
  top: 10%;
}
.swiper-slide:nth-child(2n + 3) .card {
  border: 5px solid magenta;

  position: absolute;
  top: 20%;
}

.swiper-slide {
  font-size: 18px;
  color: #fff;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  /* padding: 40px 60px; */
  width: 100%;

  .card {
    width: 85%;
    height: 50%;
  }

  img {
    width: 100%;
    height: 100%;

    position: absolute;
  }
  .title {
    font-family: 'Archivo Black', sans-serif;

    font-size: 17px;
    font-weight: 1000;

    position: absolute;
    top: 60%;
    left: 0px;
  }
  .subtitle {
    font-family: 'Archivo Black', sans-serif;
    font-size: 65px;

    position: absolute;
    top: 62%;
    left: 0%;
    text-decoration: underline;
  }
  .text {
    font-size: 14px;
    max-width: 400px;
    line-height: 1.3;
  }

  border: 1px solid green;
}

.swiper-slide:nth-child(n + 2) {
  width: 50%;
}

.parallax-bg {
  position: absolute;
  left: 0;
  top: 0;
  width: 200%;
  height: 100%;
  -webkit-background-size: cover;
  background-size: cover;
  background-position: center;
}
</style>
