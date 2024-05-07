<script setup>
defineProps({
  title: String,
  link: String,
  logo: String,
})
</script>

<template>
  <div class="link hd">
    <a :href="link">
      <img :src="logo" alt="yt icon" height="100%" style="aspect-ratio: 1/1;" />
      <span>{{ title }}</span>
    </a>
  </div>
</template>



<style scoped>
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
  transition: all 0.3s cubic-bezier(0, 0, 0.06, 1);
}

.link:hover {
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  background: rgba(167, 91, 146, 0.144);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.37);
}
</style>