<template>
    <div id="app">
      <div class="demo-nav">
        <label>
          <span>slidesPerView:</span>
          <span class="spv">{{ slidesPerView }}</span>
          <span class="dropdown">
            <span v-for="value in slideOptions" :key="value" @click="setSlidesPerView(value)">{{ value }}</span>
          </span>
        </label>
        <label>
          <input type="checkbox" v-model="centeredSlides" />
          <span>centeredSlides</span>
        </label>
      </div>
      <div class="demo-slider swiper-slide-active">
        <swiper :slides-per-view="slidesPerView" :centered-slides="centeredSlides" :space-between="30" class="swiper">
          <swiper-slide v-for="(slide, index) in slides" :key="index">
            <div class="swiper-material-wrapper">
              <div class="object-fill swiper-material-content h-fit">
                <img :src="slide.image" class="demo-material-image rounded-3xl" data-swiper-material-scale="1.75" />
                <span class="demo-material-label swiper-material-animate-opacity">{{ slide.label }}</span>
              </div>
            </div>
          </swiper-slide>
        </swiper>
      </div>
    </div>
  </template>
  
  <script>
  import { Swiper, SwiperSlide } from 'swiper/vue';
  import 'swiper/swiper-bundle.css';
  
  export default {
    components: {
      Swiper,
      SwiperSlide,
    },
    data() {
      return {
        slidesPerView: 3,
        centeredSlides: true,
        slideOptions: [1, 2, 3, 4, 5],
        slides: [
          { image: 'https://material-you-slider.uiinitiative.com/images/01.jpg', label: 'Slide 1' },
          { image: 'https://material-you-slider.uiinitiative.com/images/02.jpg', label: 'Slide 2' },
          { image: 'https://material-you-slider.uiinitiative.com/images/03.jpg', label: 'Slide 3' },
          { image: 'https://material-you-slider.uiinitiative.com/images/04.jpg', label: 'Slide 4' },
          { image: 'https://material-you-slider.uiinitiative.com/images/05.jpg', label: 'Slide 5' },
          { image: 'https://material-you-slider.uiinitiative.com/images/06.jpg', label: 'Slide 6' },
          { image: 'https://material-you-slider.uiinitiative.com/images/07.jpg', label: 'Slide 7' },
          { image: 'https://material-you-slider.uiinitiative.com/images/08.jpg', label: 'Slide 8' },
          { image: 'https://material-you-slider.uiinitiative.com/images/09.jpg', label: 'Slide 9' },
          { image: 'https://material-you-slider.uiinitiative.com/images/10.jpg', label: 'Slide 10' },
        ],
      };
    },
    methods: {
      setSlidesPerView(value) {
        this.slidesPerView = value;
      },
    },
  };
  </script>
  
  <style scoped>
  .demo-nav {
    display: flex;
    justify-content: space-between;
    margin-bottom: 10px;
  }
  
  .demo-slider {
    width: 100%;
    margin: 50px auto;
  }
  
  .swiper-material-wrapper img {
    position: relative;
    height: 450px;
    object-fit: cover;
  }
  
  .demo-material-image {
    width: 100%;
    height: auto;
  }
  
  .demo-material-label {
    position: absolute;
    bottom: 20px;
    left: 20px;
    color: white;
    font-size: 1.5rem;
  }
  </style>
  