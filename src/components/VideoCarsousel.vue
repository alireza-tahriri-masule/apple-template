<script>
import { hightlightsSlides } from "../constants";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Autoplay, Pagination } from 'swiper/modules';

// Import Swiper styles
import "swiper/css";
import 'swiper/css/pagination';
import 'swiper/css/navigation';
import 'swiper/swiper-bundle.css';

export default {
  data() {
    return {
      slides: [],
      progress: 1,
      progressTimeLeft: 0, // Time left for autoplay
      modules: [Pagination, Autoplay], // Swiper modules
    };
  },
  components: {
    Swiper,
    SwiperSlide,
  },
  methods: {
    onAutoplayTimeLeft(swiper, time, progress) {
      this.progressTimeLeft = Math.ceil(time / 1000); // Update the time left in seconds
      this.progress = progress; // Set the progress value for the circle
    },
  },
  mounted() {
    this.slides = hightlightsSlides;
  },
};
</script>

<template>
  <swiper
    :slidesPerView="'auto'"
    :spaceBetween="30"
    :pagination="{
      clickable: true,
    }"
    :modules="modules"
    :loop="true"
    :autoplay="{ delay: 2500, disableOnInteraction: false }"
    @autoplayTimeLeft="onAutoplayTimeLeft" 
    class="overflow-hidden rounded-3xl mySwiper"
  >
    <swiper-slide class="flex items-center" 
      v-for="slide in slides"
      :key="slide.id"
      id="slider">
      <div>
        <div class="object-cover overflow-hidden bg-black flex-center">
          <video id="video" playsinline preload="auto" muted autoplay loop class="w-full h-[550px] scale-110">
            <source :src="slide.video" type="video/mp4"></source>
          </video>
        </div>

        <div class="absolute top-12 left-[5%] z-10">
          <p v-text="text" v-for="text in slide.textLists" class="text-xl font-medium md:text-2xl"></p>
        </div>
      </div>
      <div class="absolute z-10 flex items-center justify-center autoplay-progress bottom-4 right-4">
        <svg width="48" height="48" viewBox="0 0 48 48" class="relative">
          <circle
            cx="24"
            cy="24"
            r="20"
            stroke="#fff"
            stroke-width="4"
            fill="none"
            stroke-dasharray="126" 
            :stroke-dashoffset="120 * (1 - progress)"
            class="progress-circle"
          ></circle>
          <!-- Time in the center of the circle -->
          <text x="50%" y="50%" text-anchor="middle" dy=".3em" font-size="14" fill="#fff">{{ progressTimeLeft }}s</text>
        </svg>
      </div>
    </swiper-slide>
  </swiper>
</template>

<style>
.swiper-pagination-bullet {
  width: 18px !important;
  height: 10px !important;
  border-radius: 3px !important;
  background-color: #fff !important;
}

.progress-circle {
  transform: rotate(-90deg);
  transform-origin: center;
}
</style>
