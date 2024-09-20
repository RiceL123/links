<script setup>
import { onMounted, ref } from 'vue'

defineProps({
  title: String,
  link: String,
  svg_color: String,
})

let boundingReg = ref(null)

const linkNode = ref()
onMounted(() => {
  linkNode.value.style.transform = 'translate(-2000px, -500px) scale(.5) rotate(-90deg)'
  linkNode.value.style.opacity = 0;
})
</script>

<template>
  <div ref='linkNode' class="link" @mouseenter="e => {
    boundingReg = e.currentTarget.getBoundingClientRect();
    const svgPaths = e.target.querySelectorAll('path, polygon, rect, line, polyline, circle');
    svgPaths.forEach(path => {
      const length = 200;
      path.style.strokeDasharray = 50;
      path.style.strokeDashoffset = length;
      path.style.transition = 'stroke-dashoffset 2s ease-in-out, stroke 0.4s ease-in-out';
      path.style.stroke = svg_color;
    });

  }" @mouseleave="e => {
    boundingReg = null;
    e.currentTarget.style.setProperty('transform', 'translate(0, 0) scale(1) rotate(0)');
    const svgPaths = e.target.querySelectorAll('path, polygon, rect, line, polyline, circle');
    svgPaths.forEach(path => {
      path.style.transition = 'stroke-dashoffset 1.5s ease-in-out, stroke 2s ease-in';
      path.style.strokeDashoffset = 0;
      path.style.strokeDasharray = path.getTotalLength();
      path.style.stroke = '#202020';
    });
  }" @mousemove="e => {
    if (boundingReg) {
      const x = e.clientX - boundingReg.left;
      const y = e.clientY - boundingReg.top;
      const xPercentage = x / boundingReg.width;
      const yPercentage = y / boundingReg.height;
      const xRotation = (xPercentage - 0.5) * 10;
      const yRotation = (0.5 - yPercentage) * 10;
      e.currentTarget.style.setProperty('transform', `perspective(100px) rotateY(${xRotation}deg) rotateX(${yRotation}deg`);

      const linkText = e.currentTarget.lastChild.lastChild;
      linkText.style.textShadow = `rgba(255, 0, 0, 0.4) ${xRotation}px ${-yRotation}px, rgba(0, 255, 255, 0.5) ${-xRotation}px ${yRotation}px, black 2px 2px`;
    }
  }">
    <a :href="link"
      style="cursor: inherit; display: flex; align-items: center; gap: 1rem; text-decoration: none; color: black; width: 100%">

      <slot></slot> <!-- svg component here -->

      <p class="link-text">{{ title }}</p>
    </a>
  </div>
</template>

<style scoped>
.link {
  max-width: 70vw;
  display: flex;
  height: 4.5em;
  border-radius: 1em;
  padding: 1em;
  background: rgba(155, 148, 153, 0.192);
  border-radius: 16px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(3px);
  -webkit-backdrop-filter: blur(3px);
  transition: all 0.2s;
  cursor: url(https://raw.githubusercontent.com/RiceL123/links/master/src/assets/cursor.png) 12 0, auto;

  fill: none;
  stroke-linecap: round;
  stroke-linejoin: round;

  stroke: #202020;
  stroke-width: 1.5px;

  transform: translate(-2000px, -500px) scale(.5) rotate(-90deg);
}

.link:hover,
.link:focus {
  opacity: 1 !important;
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  background: rgba(167, 91, 146, 0.144);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.37);
  scale: 1.1;
}

.link-text {
  color: azure;
  font-size: larger;
  font-weight: bolder;
  text-shadow: rgba(255, 0, 0, 0.4) 3px -2px, rgba(0, 255, 255, 0.5) -3px 3px, black 2px 2px;
}
</style>
