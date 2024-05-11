<script setup>
import WebLink from './components/WebLink.vue'
import { onMounted, ref, toRaw } from 'vue'

const items = ref([
  {
    title: 'Websit',
    link: 'https://ricel123.netlify.app/',
    logo: 'https://files.catbox.moe/oi37kr.png'
  },
  {
    title: 'Youtube',
    link: 'https://www.youtube.com/@RiceL123',
    logo: 'https://raw.githubusercontent.com/RiceL123/links/master/src/assets/yt.svg'
  },
  {
    title: 'Github',
    link: 'https://github.com/ricel123',
    logo: 'https://raw.githubusercontent.com/RiceL123/links/master/src/assets/github.svg'
  },
  {
    title: 'Twitch',
    link: 'https://www.twitch.tv/ricel12345',
    logo: 'https://raw.githubusercontent.com/RiceL123/links/master/src/assets/twitch.svg'
  },
  {
    title: 'Instagram',
    link: 'https://www.instagram.com/ricel12345/',
    logo: 'https://raw.githubusercontent.com/RiceL123/links/master/src/assets/insta.svg'
  },
  {
    title: 'Twitter',
    link: 'https://twitter.com/ricel123',
    logo: 'https://raw.githubusercontent.com/RiceL123/links/master/src/assets/twitter.svg'
  },
  {
    title: 'My AnimeList',
    link: 'https://myanimelist.net/profile/Ricel123',
    logo: 'https://raw.githubusercontent.com/RiceL123/links/master/src/assets/anime.svg'
  },
  {
    title: 'Jstris',
    link: 'https://jstris.jezevec10.com/u/RiceL123',
    logo: 'https://raw.githubusercontent.com/RiceL123/links/master/src/assets/jstris.svg'
  },
  {
    title: 'tetrio',
    link: 'https://ch.tetr.io/u/ricel123',
    logo: 'https://raw.githubusercontent.com/RiceL123/links/master/src/assets/tetrio.svg'
  },
  {
    title: 'osu',
    link: 'https://osu.ppy.sh/users/16549400',
    logo: 'https://raw.githubusercontent.com/RiceL123/links/master/src/assets/osu.svg'
  },
  {
    title: 'spotify',
    link: 'https://open.spotify.com/user/75ugbigv9cpu446t1pctxw0rl?si=69cde5aae58142c5',
    logo: 'https://raw.githubusercontent.com/RiceL123/links/master/src/assets/spotify.svg'
  },
  {
    title: 'sheet',
    link: 'https://docs.google.com/spreadsheets/d/1_fq3KERt8A-90-qOTUsP87QtQFZgj6aZ-3efs_eJkMg/edit?usp=sharing',
    logo: 'https://raw.githubusercontent.com/RiceL123/links/master/src/assets/sheet.svg'
  },
  {
    title: 'reddit',
    link: 'https://www.reddit.com/user/RiceL123/',
    logo: 'https://raw.githubusercontent.com/RiceL123/links/master/src/assets/reddit.svg'
  },

])

const linkRefs = ref([])

onMounted(() => window.addEventListener("mousemove", (e) => perpective_background(e)));

let link_nodes = [];
let background;
let girl;
onMounted(() => {
  link_nodes = document.querySelectorAll(".link");
  background = document.getElementById('background');
  girl = document.getElementById('girl');
});

const perpective_background = (e) => {  
  const clamp = 3;
  const mouse_x = e.clientX;
  const mouse_y = e.clientY;

  let center_y = window.innerHeight / 2;
  let center_x = window.innerWidth / 2;
  let yRotation = Math.max(-clamp, Math.min(((mouse_x - center_x) / center_x) * clamp, clamp));
  let xRotation = Math.max(-clamp, Math.min(((mouse_y - center_y) / center_y) * clamp, clamp));
  background.style.transform = `perspective(1000px) rotateX(${xRotation}deg) rotateY(${yRotation}deg)`;
  girl.style.transform = `perspective(1000px) rotateX(${-xRotation * 0.5}deg)  rotateY(${-yRotation * 0.5}deg)`;
}
</script>

<template>
  <div
    style="position: absolute; height: 100vh; width: 100vw; z-index: -10; overflow: hidden; display: flex; justify-content: center;">
    <img id="background" src="https://files.catbox.moe/kp1hqu.png" alt="background" height="100%" style="transition: all 0.1s; scale: 1.2;">
  </div>
  <div
    style="position: absolute; height: 100vh; width: 100vw; z-index: -5; overflow: hidden; display: flex; justify-content: center;">
    <img id="girl" src="https://files.catbox.moe/rxuihd.png" alt="background girl" height="100%" style="transition: all 0.1s; scale: 1.2;">
  </div>

  <header>
    <h2>Links for RiceL123</h2>
  </header>

  <div id="link-container">
    <WebLink v-for="item in items" :title="item.title" :link="item.link" :logo="item.logo"></WebLink>
  </div>

  <p style="place-self: end; padding-right: 1rem; font-size: smaller;">background art by me 💀</p>
</template>

<style scoped>
@media (min-width: 600px) {
  #link-container {
    gap: 2em;
    display: grid;
    grid-template-areas:
      "main main . main main"
      "main main . main main"
      "main main main main main";
    grid-template-columns: repeat(3, 1fr);
    grid-auto-rows: minmax(80px, auto);
  }
}

@media (min-width: 1000px) {
  #link-container {
    grid-template-columns: repeat(5, 1fr);
    grid-auto-rows: minmax(100px, auto);
  }
}

/* #link-container:hover .link:not(:hover) {
  opacity: 0.2;
  transition: all 0.5s ease-in-out;
} */
</style>