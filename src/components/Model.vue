<script>
import gsap from "gsap";
import ModelView from "./ModelView.vue";
import { ref, reactive, onMounted } from "vue";
import * as THREE from "three";
import { yellowImg } from "../utils";
import { models, sizes } from "../constants";

export default {
  data() {
    return {
      size: "small",
      model: {
        title: "iPhone 15 Pro in Natural Titanium",
        color: ["#8F8A81", "#FFE7B9", "#6F6C64"],
        img: yellowImg,
      },
      models: models,
      sizes: sizes,
    };
  },
  methods: {
    setModel(value) {
      this.model = value;
    },
    setSize(value) {
      this.size = value;
    },
  },
  components: {
    ModelView,
  },
  mounted() {
    gsap.to("#heading", { y: 0, opacity: 1 });
  },
  setup() {
    // Use reactive for managing objects like `model`
    // const model = reactive({
    //   title: "iPhone 15 Pro in Natural Titanium",
    //   color: ["#8F8A81", "#FFE7B9", "#6F6C64"],
    //   img: yellowImg,
    // });

    // Camera controls (assuming they might be DOM elements or three.js objects)
    const cameraControlSmall = ref(null);
    const cameraControlLarge = ref(null);

    // Example of a three.js group in Vue
    const small = ref(new THREE.Group());
    const large = ref(new THREE.Group());

    // Define smallRotation and largeRotation as reactive references
    const smallRotation = ref(0);
    const largeRotation = ref(0);

    function setSmallRotation(newRotation) {
      smallRotation.value = newRotation;
    }

    function setLargeRotation(newRotation) {
      largeRotation.value = newRotation;
    }

    // onMounted lifecycle hook to handle actions after the component is mounted
    onMounted(() => {
      // Add any initialization logic, for example setting up the camera controls or three.js scene
    });

    return {
      cameraControlSmall,
      cameraControlLarge,
      small,
      large,
    };
  },
};
</script>

<template>
  <section class="common-padding">
    <div class="screen-max-width">
      <h1 id="heading" class="section-heading">Take a closer look.</h1>

      <div class="flex flex-col items-center mt-5">
        <div
          class="w-full h-[75vh] md:h-[85vh] overflow-hidden relative"
        >
          <ModelView />
        </div>

        <div class="w-full mx-ato">
          <p class="mb-5 text-sm font-light text-center" v-text="model.title"></p>

          <div class="flex-center">
            <ul class="color-container">
              <li
                class="w-6 h-6 mx-2 rounded-full cursor-pointer"
                :style="{ backgroundColor: item.color }"
                v-for="item in models"
                @click="setModel(item)"
              ></li>
            </ul>

            <button class="size-btn-container">
              <span
                v-for="item in sizes"
                v-text="item.label"
                class="size-btn"
                :style="{
                  backgroundColor: size === item.value ? 'white' : 'transparent',
                  color: size === item.value ? 'black' : 'white',
                }"
                @click="setSize(item.value)"
              ></span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped></style>
