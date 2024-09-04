<script>
import { gsap } from "gsap";
import { ref, computed, onMounted, watchEffect } from 'vue';
import { heroVideo, smallHeroVideo } from "../utils";

export default {
  setup() {
    const videoSrc = ref(window.innerWidth < 760 ? smallHeroVideo : heroVideo);

    // برای به‌روزرسانی ویدیو بر اساس تغییر اندازه صفحه
    const updateVideoSrc = () => {
      videoSrc.value = window.innerWidth < 760 ? smallHeroVideo : heroVideo;
    };

    watchEffect(() => {
      window.addEventListener('resize', updateVideoSrc);
    });

    onMounted(() => {
      gsap.to("#hero", { opacity: 1, delay: 2 });
      gsap.to("#cta", { opacity: 1, y: -50, delay: 2 });
    });

    return {
      videoSrc: computed(() => videoSrc.value)
    };
  },
};
</script>

<template>
  <section class="w-full nav-height bg-black relative">
    <div class="h-5/6 w-full flex-center flex-col">
      <p id="hero" class="hero-title">iPhone 15 Pro</p>
      <div class="md:w-10/12 w-9/12">
        <video class="pointer-events-none" autoplay muted playsinline="true" :key="videoSrc">
          <source :src="videoSrc" type="video/mp4" />
        </video>
      </div>
    </div>

    <div id="cta" class="flex flex-col items-center opacity-0 translate-y-20">
        <a href="#hightlights" class="btn">Buy</a>
        <p class="font-normal text-xl">From $199/month or $999</p>
    </div>
  </section>
</template>

<style scoped></style>
