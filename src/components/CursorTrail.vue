<script setup>
import { onMounted } from 'vue'

let canvas;
let ctx;
let width;
let height;

let stars = [];
let lastMouseX = 0;
let lastMouseY = 0;
let mouseVelocityX = 0;
let mouseVelocityY = 0;
onMounted(() => {
  canvas = document.getElementById("trailCanvas");
  ctx = canvas.getContext('2d');

  width = canvas.width = window.innerWidth;
  height = canvas.height = window.innerHeight;

  window.addEventListener('resize', function () {
    width = canvas.width = window.innerWidth;
    height = canvas.height = window.innerHeight;
  });
  window.addEventListener("mousemove", drawTrail);
  update();
})

class Star {
  constructor(x, y, velocityX, velocityY) {
    this.x = x;
    this.y = y;
    this.finalSize = Math.random() * 2;
    this.size = this.finalSize * 2;
    this.red = (Math.random() * 255) % 55 + 155;
    this.green = (Math.random() * 255) % 55 + 120;
    this.blue = (Math.random() * 255) % 55 + 200;
    this.alpha = Math.random() * 0.5 + 0.5;
    this.velocityX = velocityX * 0.05;
    this.velocityY = 1 + Math.random() + velocityY * 0.05;
    this.gravity = 0.02;
    this.drag = 0.97;
    this.turbulence = () => Math.random() * 0.5 - 0.25;
    this.timeElapsed = 0;
  }
  draw() {
    ctx.fillStyle = `rgba(${this.red}, ${this.green}, ${this.blue}, ${this.alpha})`;
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
    ctx.fill();
  }

  update(deltaTime) {
    this.x += this.velocityX + this.turbulence();
    this.velocityX *= this.drag;
    this.y += this.velocityY;
    this.velocityY += this.gravity;
    this.alpha = Math.max(0, this.alpha - 0.005);

    this.timeElapsed += deltaTime;
    if (this.timeElapsed < 2000) {
      this.size = this.finalSize * 2 - (this.finalSize * this.timeElapsed / 2000);
    } else {
      this.size = this.finalSize;
    }
  }
}

const drawTrail = (e) => {
  mouseVelocityX = e.clientX - lastMouseX;
  mouseVelocityY = e.clientY - lastMouseY;
  lastMouseX = e.clientX;
  lastMouseY = e.clientY;

  let randomOffsetX = (Math.random() - 0.5) * 100;
  let randomOffsetY = (Math.random() - 0.5) * 100;

  stars.push(new Star(e.clientX, e.clientY, mouseVelocityX + randomOffsetX, mouseVelocityY + randomOffsetY));
}

let lastTime = 0;

function update(time = 0) {
  const deltaTime = time - lastTime;
  lastTime = time;

  ctx.clearRect(0, 0, width, height);
  stars.forEach(star => star.update(deltaTime));
  stars.forEach(star => star.draw());
  stars = stars.filter(star => star.alpha > 0 && star.y < height && star.x > 0 && star.x < width);
  requestAnimationFrame(update);
}
</script>

<template>
  <canvas id="trailCanvas" style="position: absolute; top: 0; left: 0; z-index: -1;"></canvas>
</template>

<style></style>