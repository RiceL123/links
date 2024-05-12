<script setup>
import { ref } from 'vue'
defineProps({
  title: String,
  link: String,
  logo: String,
})

let boundingReg = ref(null)
</script>

<template>
  <div class="link" 
    @mouseenter="(e) => boundingReg = e.currentTarget.getBoundingClientRect()"  
    @mouseleave="e => { boundingReg = null; e.currentTarget.style.setProperty('transform', ''); }" 
    @mousemove="(e) => {
      if (boundingReg) {
        const x = e.clientX - boundingReg.left;
        const y = e.clientY - boundingReg.top;
        const xPercentage = x / boundingReg.width;
        const yPercentage = y / boundingReg.height;
        const xRotation = (xPercentage - 0.5) * 10;
        const yRotation = (0.5 - yPercentage) * 10;
        e.currentTarget.style.setProperty('transform', `perspective(100px) rotateY(${xRotation}deg) rotateX(${yRotation}deg`);
      }
    }">
    <a :href="link"
      style="cursor: inherit; display: flex; align-items: center; gap: 1rem; text-decoration: none; color: black; width: 100%">
      <img class="link-img" :src="logo" alt="yt icon" height="100%" style="aspect-ratio: 1/1;" />
      <p>{{ title }}</p>
    </a>
  </div>
</template>

<style scoped>
.link {
  display: flex;
  height: 5em;
  border-radius: 1em;
  padding: 1em;
  background: rgba(167, 91, 145, 0.048);
  border-radius: 16px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(3px);
  -webkit-backdrop-filter: blur(3px);
  transition: all 0.1s;
  cursor: url(https://raw.githubusercontent.com/RiceL123/links/master/src/assets/cursor.png) 12 0, auto;
}

.link:hover {
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
  background: rgba(167, 91, 146, 0.144);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.37);
  scale: 1.1;
}
</style>