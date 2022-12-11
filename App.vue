<template>
  <div class="home">
    <div class="canvas-container" ref="canvasDom">
      <div class="select">
        <span class="first">颜色选择</span>
        <div class="select-box">
          <span class="text">前脸</span>
          <div class="color">
            <div class="red" id="font-red" @click="changeColor($event)"></div>
            <div class="yellow" id="font-yellow" @click="changeColor($event)"></div>
            <div class="white" id="font-white" @click="changeColor($event)"></div>
          </div>
        </div>
        <div class="select-box">
          <span class="text">侧面</span>
          <div class="color">
            <div class="red" id="side-red" @click="changeColor($event)"></div>
            <div class="yellow" id="side-yellow" @click="changeColor($event)"></div>
            <div class="white" id="side-white" @click="changeColor($event)"></div>
          </div>
        </div>
        <div class="select-box">
          <span class="text">尾翼及镜子</span>
          <div class="color">
            <div class="red" id="tail-red" @click="changeColor($event)"></div>
            <div class="yellow" id="tail-yellow" @click="changeColor($event)"></div>
            <div class="white" id="tail-white" @click="changeColor($event)"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";
import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader";
import { DRACOLoader } from "three/examples/jsm/loaders/DRACOLoader"

export default {
  data() {
    return {
      camera: null,
      scene: null,
      renderer: null,
      mesh: null,
      controls: null,
      bmw: null,
    };
  },
  mounted() {
    this.init();
    this.render();
  },
  methods: {
    init() {
      let canvasDom = this.$refs.canvasDom;
      //场景
      this.scene = new THREE.Scene();
      //相机
      this.camera = new THREE.PerspectiveCamera(
        45,
        window.innerWidth / window.innerHeight,
        0.1,
        200
      );
      this.camera.position.set(3, 3.5, 6);
      //渲染器
      this.renderer = new THREE.WebGLRenderer({
        //抗锯齿
        antialias: true,
      });
      //渲染器尺寸
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      //将渲染器加入到页面
      canvasDom.appendChild(this.renderer.domElement);
      //设置渲染背景
      this.renderer.setClearColor("#000");
      this.scene.background = new THREE.Color("#ccc");
      this.scene.environment = new THREE.Color("#ccc");
      //添加网格地面
      const gridHelper = new THREE.GridHelper(10, 20);
      gridHelper.material.transparent = true;
      gridHelper.material.opacity = 0.2;
      this.scene.add(gridHelper);
      //添加控制器
      this.controls = new OrbitControls(this.camera, this.renderer.domElement);
      this.controls.enableDamping = true;
      //添加模型
      const loader = new GLTFLoader();
      const dracoLoader = new DRACOLoader();
      dracoLoader.setDecoderPath("./draco/gltf/");
      loader.setDRACOLoader(dracoLoader);
      loader.load("./model/scene.gltf", (gltf) => {
        this.bmw = gltf.scene;
        this.bmw.position.set(0, 0, 0);
        this.scene.add(this.bmw);
      });
      //添加环境光 让模型显示
      let light1 = new THREE.DirectionalLight(0xffffff, 2.5);
      light1.position.set(0, 0, 10);
      this.scene.add(light1);
      let light2 = new THREE.DirectionalLight(0xffffff, 2.5);
      light2.position.set(0, 0, -10);
      this.scene.add(light2);
      let light3 = new THREE.DirectionalLight(0xffffff, 2.5);
      light3.position.set(10, 0, 0);
      this.scene.add(light3);
      let light4 = new THREE.DirectionalLight(0xffffff, 2.5);
      light4.position.set(-10, 0, 0);
      this.scene.add(light4);
      let light5 = new THREE.DirectionalLight(0xffffff, 2.5);
      light5.position.set(0, 10, 0);
      this.scene.add(light5);
    },
    render() {
      this.renderer.render(this.scene, this.camera);
      this.controls.update();
      requestAnimationFrame(this.render);
    },
    changeColor(e) {
      this.bmw.traverse((child) => {
        //前脸
        if (e.target.id === "font-red") {
          if (child.name.includes("Object_21")) {
            child.material = new THREE.MeshPhysicalMaterial({
              color: 0xff0000,
              roughness:0,
              metalness:0.5,
            });
          }
        }
        if (e.target.id === "font-yellow") {
          if (child.name.includes("Object_21")) {
            child.material = new THREE.MeshPhysicalMaterial({
              color: 0xffff00,
              roughness:0,
              metalness:0.5,
            });
          }
        }
        if (e.target.id === "font-white") {
          if (child.name.includes("Object_21")) {
            child.material = new THREE.MeshPhysicalMaterial({
              color: 0xffffff,
              roughness:0,
              metalness:0.5,
            });
          }
        }
        //侧面
        if (e.target.id === "side-red") {
          if (child.name.includes("Object_5")) {
            child.material = new THREE.MeshPhysicalMaterial({
              color: 0xff0000,
              roughness:0,
              metalness:0.5,
            });
          }
        }
        if (e.target.id === "side-yellow") {
          if (child.name.includes("Object_5")) {
            child.material = new THREE.MeshPhysicalMaterial({
              color: 0xffff00,
              roughness:0,
              metalness:0.5,
            });
          }
        }
        if (e.target.id === "side-white") {
          if (child.name.includes("Object_5")) {
            child.material = new THREE.MeshPhysicalMaterial({
              color: 0xffffff,
              roughness:0,
              metalness:0.5,
            });
          }
        }
        //尾翼
        if (e.target.id === "tail-red") {
          if (child.name.includes("Object_23")) {
            child.material = new THREE.MeshPhysicalMaterial({
              color: 0xff0000,
              roughness:0,
              metalness:0.5,
            });
          }
        }
        if (e.target.id === "tail-yellow") {
          if (child.name.includes("Object_23")) {
            child.material = new THREE.MeshPhysicalMaterial({
              color: 0xffff00,
              roughness:0,
              metalness:0.5,
            });
          }
        }

        if (e.target.id === "tail-white") {
          if (child.name.includes("Object_23")) {
            child.material = new THREE.MeshPhysicalMaterial({
              color: 0xffffff,
              roughness:0,
              metalness:0.5,
            });
          }
        }
      });
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
.select {
  padding: 10px 30px 20px 30px;
  border: 3px solid white;
  border-radius: 15px;
  position: fixed;
  top: 50px;
  right: 100px;
}
.select-box {
  margin-top: 10px;
}
.first {
  color: white;
  font-size: 20px;
  font-weight: bold;
  padding-bottom: 5px;
  border-bottom: 2px solid white;
}
.red {
  width: 20px;
  height: 20px;
  background-color: red;
  border: 2px solid rgb(228, 228, 228);
  border-radius: 5px;
}
.yellow {
  width: 20px;
  height: 20px;
  background-color: rgb(253, 253, 25);
  border: 2px solid rgb(228, 228, 228);
  border-radius: 5px;
}
.white {
  width: 20px;
  height: 20px;
  background-color: white;
  border: 2px solid rgb(228, 228, 228);
  border-radius: 5px;
}
.text {
  color: white;
  font-size: 20px;
  padding-top: 5px;
  font-weight: bold;
  padding-bottom: 5px;
  border-bottom: 2px solid white;
}
.color {
  display: flex;
  margin-top: 15px;
  justify-content: space-around;
}
</style>
