<script setup>
import WebLink from './components/WebLink.vue'
import CursorTrail from './components/CursorTrail.vue'
import { onMounted, ref } from 'vue'
import { reactive } from 'vue';

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
]);

let background;
let girl;
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
      girl.style.transform = `perspective(1000px) rotateX(${-xRotation * 0.5}deg)  rotateY(${-yRotation * 0.5}deg)`;
    }
  });

  background = document.getElementById('background');
  girl = document.getElementById('girl');
});

const heroAndBack = reactive([
  ["https://raw.githubusercontent.com/RiceL123/links/master/src/assets/hero.png", "https://raw.githubusercontent.com/RiceL123/links/master/src/assets/background.png"],
  ["https://raw.githubusercontent.com/RiceL123/links/master/src/assets/hero_1.png", "https://raw.githubusercontent.com/RiceL123/links/master/src/assets/background_1.png"]
]);

let index = ref(0);
</script>

<template>
  <Transition name="slide-down" appear>
    <div
      style="position: absolute; height: 100vh; width: 100vw; z-index: -10; overflow: hidden; display: flex; justify-content: center;">
      <img id="background" :src="heroAndBack[index][1]"
        alt="background" height="100%" style="transition: all 0.1s; scale: 1.2;">
    </div>
  </Transition>
  <Transition name="slide-up" appear>
    <div
      style="position: absolute; height: 100vh; width: 100vw; z-index: -5; overflow: hidden; display: flex; justify-content: center;">
      <img id="girl" :src="heroAndBack[index][0]"
        alt="background girl" height="100%" style="transition: all 0.1s; scale: 1.2;">
    </div>
  </Transition>
  <CursorTrail></CursorTrail>

  <header style="display: flex; flex-direction: column; align-items: center;">
    <h1>Links for RiceL123</h1>
  </header>

  <div id="link-container">
    <WebLink v-for="item in items" :title="item.title" :link="item.link" :logo="item.logo"></WebLink>
  </div>

  <p class="tooltip" style="place-self: end; padding-right: 1rem; font-size: smaller; background-color: rgba(255, 255, 255, 0.3); padding: 5px; border-radius: 5px;" @click="index = (index + 1) % heroAndBack.length">
    background art by me 💀
    <span class="tooltiptext">cursor and icons as well 😁</span>
  </p>
</template>

<style scoped>
#link-container {
  display: flex;
  flex-direction: column;
  gap: 1em;
  max-width: 2000px;
  margin-inline: 3em;
}

@media (min-width: 1100px) {
  #link-container {
    display: grid;
    grid-template-columns: repeat(3, minmax(300px, 1fr));
    grid-auto-rows: minmax(80px, auto);
  }
}

@media (min-width: 1400px) {
  #link-container {
    display: grid;
    grid-template-columns: repeat(5, minmax(200px, 1fr));
    grid-auto-rows: minmax(80px, auto);
  }
}

#link-container:hover .link:not(:hover) {
  opacity: 0.2;
  transition: all 0.5s ease-in-out;
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

.slide-down-enter-active {
  transition: all 2s cubic-bezier(.21, .61, .21, 1.03);
}

.slide-down-enter-from {
  transform: translateY(-200px);
  opacity: 0.4;
}

.slide-up-enter-active {
  transition: all 2s cubic-bezier(.21, .61, .21, 1.03);
}

.slide-up-enter-from {
  transform: translateY(200px);
  opacity: 0.4;
}
</style>