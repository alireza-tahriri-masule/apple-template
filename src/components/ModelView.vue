<template>
  <div id="container3D"></div>
</template>

<script>
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";
import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader";
import { markRaw } from "vue"; // Import markRaw from Vue

export default {
  data() {
    return {
      scene: markRaw(new THREE.Scene()), // Mark the scene as non-reactive
      camera: markRaw(
        new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
      ),
      renderer: null,
      controls: null,
      object: null,
      mouseX: window.innerWidth / 2,
      mouseY: window.innerHeight / 2,
      objToRender: "iphone", // The object you want to render
    };
  },
  mounted() {
    this.initThreeJS();
    this.animate();
    window.addEventListener("resize", this.onWindowResize);
    document.addEventListener("mousemove", this.onMouseMove);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.onWindowResize);
    document.removeEventListener("mousemove", this.onMouseMove);
  },
  methods: {
    initThreeJS() {
      // Renderer
      this.renderer = new THREE.WebGLRenderer({ alpha: true });
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      document.getElementById("container3D").appendChild(this.renderer.domElement);

      // Camera position
      this.camera.position.z = this.objToRender === "iphone" ? 0.16 : 500;

      // Lights
      const topLight = new THREE.DirectionalLight(0xffffff, 1);
      topLight.position.set(500, 500, 500);
      this.scene.add(topLight);

      const ambientLight = new THREE.AmbientLight(
        0x333333,
        this.objToRender === "iphone" ? 5 : 1
      );
      this.scene.add(ambientLight);

      // Orbit Controls
      if (this.objToRender === "iphone") {
        this.controls = new OrbitControls(this.camera, this.renderer.domElement);
      }

      // Load 3D model
      const loader = new GLTFLoader();
      loader.load(
        `models/${this.objToRender}/scene.gltf`,
        (gltf) => {
          this.object = markRaw(gltf.scene); // Mark the loaded object as non-reactive
          this.scene.add(this.object);
        },
        (xhr) => {
          console.log((xhr.loaded / xhr.total) * 100 + "% loaded");
        },
        (error) => {
          console.error("An error occurred loading the model", error);
        }
      );
    },
    animate() {
      requestAnimationFrame(this.animate);
      if (this.object && this.objToRender === "eye") {
        this.object.rotation.y = -3 + (this.mouseX / window.innerWidth) * 3;
        this.object.rotation.x = -1.2 + (this.mouseY * 2.5) / window.innerHeight;
      }
      this.renderer.render(this.scene, this.camera);
    },
    onWindowResize() {
      this.camera.aspect = window.innerWidth / window.innerHeight;
      this.camera.updateProjectionMatrix();
      this.renderer.setSize(window.innerWidth, window.innerHeight);
    },
    onMouseMove(event) {
      this.mouseX = event.clientX;
      this.mouseY = event.clientY;
    },
  },
};
</script>

<style scoped>
#container3D {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
