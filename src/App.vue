<script>
  import Navbar from "./components/Navbar.vue";
  import Hero from "./components/Hero.vue";
  import Highlights from "./components/Highlights.vue";

  export default {
    components: {
      Navbar,
      Hero,
      Highlights
    }
  }
</script>

<template>
  <main class="bg-black">
    <Navbar />
    <Hero />
    <Highlights />
  </main>
</template>

<style scoped></style>
