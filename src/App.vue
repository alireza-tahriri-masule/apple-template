<script>
import Navbar from "./components/Navbar.vue";
import Hero from "./components/Hero.vue";
import Highlights from "./components/Highlights.vue";
import Model from "./components/Model.vue";

export default {
  components: {
    Navbar,
    Hero,
    Highlights,
    Model,
  },
};
</script>

<template>
  <main class="bg-black">
    <Navbar />
    <Hero />
    <Highlights />
    <Model />
  </main>
</template>

<style scoped></style>
