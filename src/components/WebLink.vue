<script setup>
defineProps({
  title: String,
  link: String,
  logo: String,
})

// const increment_count = (link) => {
//   console.log(link);
// }
</script>

<template>
  <div class="link" ref="">
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
  transition: all 1s;
}

.link:hover {
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  background: rgba(167, 91, 146, 0.144);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.37);
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