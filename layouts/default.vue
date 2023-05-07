<template>
  <div id="app">
    <div ref="container" class="container"></div>
  </div>
</template>

<script>
import * as THREE from "three";

export default {
  name: "App",
  data() {
    return {
      scene: null,
      camera: null,
      renderer: null,
      decahedron: null,
    };
  },
  mounted() {
    this.initScene();
    this.animate();
  },
  methods: {
    initScene() {
      // Set up the scene, camera, and renderer
      this.scene = new THREE.Scene();
      this.camera = new THREE.PerspectiveCamera(
        75,
        window.innerWidth / window.innerHeight,
        0.1,
        1000
      );
      this.renderer = new THREE.WebGLRenderer();
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      this.$refs.container.appendChild(this.renderer.domElement);

      // Create a decahedron geometry and material
      const geometry = new THREE.DodecahedronGeometry(2);
      const material = new THREE.MeshBasicMaterial({
        color: 0x00ff00,
        wireframe: true,
      });

      // Create a decahedron mesh
      this.decahedron = new THREE.Mesh(geometry, material);
      this.scene.add(this.decahedron);

      // Position the camera
      this.camera.position.z = 5;
    },
    animate() {
      requestAnimationFrame(this.animate);

      // Rotate the decahedron
      this.decahedron.rotation.x += 0.01;
      this.decahedron.rotation.y += 0.01;

      this.renderer.render(this.scene, this.camera);
    },
  },
};
</script>

<style>
body,
html {
  margin: 0;
  height: 100%;
}

.container {
  width: 100%;
  height: 100%;
}
</style>
