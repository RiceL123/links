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

onMounted(() => window.addEventListener("mousemove", (e) => calculate_skew(e)));

let link_nodes = [];
let background;
let girl;
onMounted(() => {
  link_nodes = document.querySelectorAll(".link");
  background = document.getElementById('background');
  girl = document.getElementById('girl');
})
const calculate_skew = (e) => {
  const clamp = 0.4;
  // linkRefs.value.forEach(link => {
  //   const mouse_x = e.clientX;
  //   const mouse_y = e.clientY;

  //   console.log(link);
  //   console.log(link.toString());
  //   // const mouse_box = toRaw(link).getBoundingClientRect();
  //   const mouse_box = { x: window.innerHeight / 2, y: window.innerWidth / 2}
  //   const center_y = mouse_box.y;
  //   const center_x = mouse_box.x;

  //   const angle = Math.atan2(mouse_y - center_y, mouse_x - center_x);

  //   link.style.transform = `rotate(${angle}rad)`;
  // });
  link_nodes.forEach(link => {
    const mouse_x = e.clientX;
    const mouse_y = e.clientY;

    const center_y = link.offsetLeft + link.offsetWidth / 2;
    const center_x = link.offsetTop + link.offsetHeight / 2;

    const angleX = Math.atan2(mouse_y - center_y, mouse_x - center_x);
    const chill_angleX = Math.max(-clamp, Math.min(angleX, clamp));

    const angleY = Math.atan(mouse_y - center_y, mouse_x - center_x);
    const chill_angleY = Math.max(-clamp, Math.min(angleY, clamp));

    link.style.transform = `perspective(500px) rotateX(${-chill_angleX}rad) rotateY(${-chill_angleY}rad)`;
  });

  // perspective of background
  let mouse_x = e.clientX;
  let mouse_y = e.clientY;

  let center_y = window.innerWidth / 2;
  let center_x = window.innerHeight / 2;

  let angleX = Math.atan2(mouse_y - center_y, mouse_x - center_x);
  let chill_angleX = Math.max(-0.1, Math.min(angleX, 0.1));

  let angleY = Math.atan(mouse_y - center_y, mouse_x - center_x);
  let chill_angleY = Math.max(-0.1, Math.min(angleY, 0.1));

  background.style.transform = `perspective(1000px) rotateX(${-chill_angleX}rad) rotateY(${-chill_angleY}rad)`;
  // perspective of girl w/ umbrella
  mouse_x = e.clientX;
  mouse_y = e.clientY;

  angleX = Math.atan2(mouse_y - center_y, mouse_x - center_x);
  chill_angleX = Math.max(-0.1, Math.min(angleX, 0.1));

  angleY = Math.atan(mouse_y - center_y, mouse_x - center_x);
  chill_angleY = Math.max(-0.1, Math.min(angleY, 0.1));

  girl.style.transform = `perspective(5000px) rotateX(${-chill_angleX}rad) rotateY(${-chill_angleY}rad)`;
}
</script>

<template>
  <div
    style="position: absolute; height: 100vh; width: 100vw; z-index: -10; overflow: hidden; display: flex; justify-content: center;">
    <img id="background" src="https://files.catbox.moe/kp1hqu.png" alt="background" height="100%" style="transition: all 1s;">
  </div>
  <div
    style="position: absolute; height: 100vh; width: 100vw; z-index: -5; overflow: hidden; display: flex; justify-content: center;">
    <img id="girl" src="https://files.catbox.moe/5vki9v.png" alt="background girl" height="100%" style="transition: all 1s;">
  </div>

  <header>
    <h2>Links for RiceL123</h2>
  </header>

  <div id="link-container">
    <WebLink v-for="item in items" :title="item.title" :link="item.link" :logo="item.logo" ref="linkRefs"></WebLink>
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

@media (min-width: 950px) {
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