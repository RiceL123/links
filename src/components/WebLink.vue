<script setup>
import { reactive, ref } from 'vue'
defineProps({
  title: String,
  link: String,
  logo: String,
})

// const increment_count = (link) => {
//   console.log(link);
// }
// onMount(() => {});
let boundingReg = ref(null)
</script>

<template>
  <div class="link" ref="linkDiv" 
    @mouseenter="(e) => boundingReg = e.currentTarget.getBoundingClientRect()"
    @mouseleave="e => { boundingReg = null; e.currentTarget.style.setProperty('transform', ''); }"
    @mousemove="(e) => {
      if (boundingReg) {
        // const clamp = 10;
        const x = e.clientX - boundingReg.left;
        const y = e.clientY - boundingReg.top;
        const xPercentage = x / boundingReg.width;
        const yPercentage = y / boundingReg.height;
        const xRotation = (xPercentage - 0.5) * 10;
        const yRotation = (0.5 - yPercentage) * 10;
        // console.log(xRotation);
        e.currentTarget.style.setProperty('transform', `perspective(100px) rotateY(${xRotation}deg) rotateX(${yRotation}deg`);
      }
    }">
    <a :href="link">
      <img class="link-img" :src="logo" alt="yt icon" height="100%" style="aspect-ratio: 1/1;" />
      <span>{{ title }}</span>
    </a>
  </div>
</template>



<style scoped>
/* .link-img {
  height: "100%"
} */

/* @media (min-width: 600px) {
  .link-img {
  height: "100%"
} */

.link {
  display: flex;
  grid-area: "main";
  height: 5em;
  border-radius: 1em;
  padding: 1em;
  background: rgba(167, 91, 145, 0.048);
  border-radius: 16px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(3px);
  -webkit-backdrop-filter: blur(3px);
  /* transition: all 0.3s cubic-bezier(0, 0, 0.06, 1); */
  transition: all 0.1s;
}

.link:hover {
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  background: rgba(167, 91, 146, 0.144);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.37);
  scale: 1.1;
}

/* .link:hover ~ .link:not(:hover) {
  opacity: 0.2;
  backdrop-filter: blur(0px);
  -webkit-backdrop-filter: blur(0px);
  background: rgba(167, 91, 146, 0.144);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.37);
} */

/* .link:hover ~ .link:hover {
  opacity: 0.2;
} */
</style>