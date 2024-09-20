<script setup>
import { onMounted, reactive, ref } from 'vue'

const show = ref(false)

const newImage = ["https://raw.githubusercontent.com/RiceL123/links/master/src/assets/hero.png", "https://raw.githubusercontent.com/RiceL123/links/master/src/assets/background.png"];
const oldImage = ["https://raw.githubusercontent.com/RiceL123/links/master/src/assets/hero_1.png", "https://raw.githubusercontent.com/RiceL123/links/master/src/assets/background_1.png"]

const heroAndBack = reactive([newImage, oldImage]);

let index = ref(0);

let background;
let hero;

onMounted(() => {

  window.addEventListener("mousemove", (e) => {
    {
      const clamp = 3;
      const mouse_x = e.clientX;
      const mouse_y = e.clientY;

      let center_y = window.innerHeight / 2;
      let center_x = window.innerWidth / 2;
      let yRotation = Math.max(-clamp, Math.min(((mouse_x - center_x) / center_x) * clamp, clamp));
      let xRotation = Math.max(-clamp, Math.min(((mouse_y - center_y) / center_y) * clamp, clamp));
      background.style.transform = `perspective(1000px) rotateX(${xRotation}deg) rotateY(${yRotation}deg)`;
      hero.style.transform = `perspective(1000px) rotateX(${-xRotation * 0.5}deg)  rotateY(${-yRotation * 0.5}deg)`;
    }
  });

  background = document.getElementById('background');
  hero = document.getElementById('hero');
});
</script>

<template>
  <Transition name="slide-down" appear>
    <div id="background-container"
      style="position: absolute; height: 100vh; width: 100vw; z-index: -10; overflow: hidden; display: flex; justify-content: center;">
      <img id="background" :src="heroAndBack[index][1]"
        alt="background" height="100%" style="transition: all 0.1s; scale: 1.2;">
    </div>
  </Transition>
  <Transition name="slide-up" appear>
    <div 
      id="hero-container"
      style="position: absolute; height: 100vh; width: 100vw; z-index: -5; overflow: hidden; display: flex; justify-content: center;">
      <img id="hero" :src="heroAndBack[index][0]"
        alt="background hero" height="100%" style="transition: all 0.1s; scale: 1.2;">
    </div>
  </Transition>
  <p class="tooltip" style="position: absolute; place-self: end; margin-right: 1rem; font-family: 'Courier New', Courier, monospace; font-size: smaller; background-color: rgba(255, 255, 255, 0.3); padding: 5px; border-radius: 5px;" @click="index = (index + 1) % heroAndBack.length">
    background art by me 💀
    <span class="tooltiptext">cursor and icons as well 😁</span>
  </p>
</template>

<style>
.slide-down-enter-active {
  transition: all 3s cubic-bezier(.21, .61, .21, 1.03);
}

.slide-down-enter-from {
  transform: translateY(-200px);
  opacity: 0.4;
}

.slide-up-enter-active {
  transition: all 3s cubic-bezier(.21, .61, .21, 1.03);
}

.slide-up-enter-from {
  transform: translateY(200px);
  opacity: 0.4;
}

.tooltip {
  position: relative;
  display: inline-block;
}

.tooltip .tooltiptext {
  visibility: hidden;
  width: 120px;
  background-color: black;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 5px 0;
  bottom: 125%;
  left: 50%;
  margin-left: -70px;
  position: absolute;
  z-index: 1;
}

.tooltip:hover .tooltiptext {
  visibility: visible;
}
</style>