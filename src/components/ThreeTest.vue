<template>
    <div id="container"></div>
  </template>
  
  <script>
  import { onMounted } from 'vue';
  import * as THREE from 'three';
  
  export default {
    name: "ThreeCube",
  
    setup() {
      let scene, camera, renderer, cube;
  
      onMounted(() => {
        init();
        animate();
      });
  
      function init() {
        // 创建场景
        scene = new THREE.Scene();
  
        // 创建相机
        camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.z = 5;
  
        // 创建渲染器
        renderer = new THREE.WebGLRenderer();
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.getElementById('container').appendChild(renderer.domElement);
  
        // 创建几何体和材质
        const geometry = new THREE.BoxGeometry();
        const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
  
        // 创建网格（Mesh）
        cube = new THREE.Mesh(geometry, material);
        scene.add(cube);
      }
  
      function animate() {
        requestAnimationFrame(animate);
  
        // 动画：旋转立方体
        cube.rotation.x += 0.01;
        cube.rotation.y += 0.01;
  
        renderer.render(scene, camera);
      }
    }
  };
  </script>
  
  <style scoped>
  #container {
    width: 100%;
    height: 100vh;
  }
  </style>