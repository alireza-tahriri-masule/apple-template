<script>
import { gsap } from "gsap";
import { rightImg, watchImg } from "../utils";
import VideoCarsousel from "./VideoCarsousel.vue";

export default {
  data() {
    return {
      rightIcon: rightImg,
      watchIcon: watchImg,
    };
  },
  components: {
    VideoCarsousel,
  },
  mounted() {
    gsap.to("#title", { opacity: 1, y: 0 });
    gsap.to(".link", { opacity: 1, y: 0, duration: 1, stagger: 0.25 });
  },
};
</script>

<template>
  <section id="highlights" class="w-screen overflow-hidden h-full common-padding bg-zinc">
    <div class="screen-max-width">
      <div class="mb-12 w-full md:flex items-end justify-between">
        <h1 id="title" class="section-heading">Get the highlights.</h1>

        <div class="flex flex-wrap items-end gap-5">
          <p class="link">
            Watch the film <img :src="watchIcon" alt="watch" class="ml-2" />
          </p>
          <p class="link">
            Watch the event <img :src="rightIcon" alt="event" class="ml-2" />
          </p>
        </div>
      </div>

      <VideoCarsousel />
    </div>
  </section>
</template>

<style scoped></style>
