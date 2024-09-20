<script setup>
import WebLink from './components/WebLink.vue'
import CursorTrail from './components/CursorTrail.vue'
import Backdrop from './components/Backdrop.vue'
import { onMounted, ref, shallowRef } from 'vue'

import Websit from './components/svgs/Websit.vue';
import Youtube from './components/svgs/Youtube.vue';
import Github from './components/svgs/Github.vue';
import Twitch from './components/svgs/Twitch.vue';
import Instagram from './components/svgs/Instagram.vue';

import Twitter from './components/svgs/Twitter.vue';
import MyAnimeList from './components/svgs/MyAnimeList.vue';
import Jstris from './components/svgs/Jstris.vue';
import Tetrio from './components/svgs/Tetrio.vue';
import osu from './components/svgs/osu.vue';

import Spotify from './components/svgs/Spotify.vue';
import sheet from './components/svgs/sheet.vue';
import Reddit from './components/svgs/Reddit.vue';

const items = shallowRef([
  {
    title: 'Websit',
    link: 'https://ricel123.netlify.app/',
    color: '#9cc2ff',
    svg_component: Websit
  },
  {
    title: 'Youtube',
    link: 'https://www.youtube.com/@RiceL123',
    color: '#ff6e6e',
    svg_component: Youtube
  },
  {
    title: 'Github',
    link: 'https://github.com/ricel123',
    color: '#84db97',
    svg_component: Github
  },
  {
    title: 'Twitch',
    link: 'https://www.twitch.tv/ricel12345',
    color: '#c693ed',
    svg_component: Twitch
  },
  {
    title: 'Instagram',
    link: 'https://www.instagram.com/ricel12345/',
    color: '#ffc38f',
    svg_component: Instagram
  },
  {
    title: 'Twitter',
    link: 'https://twitter.com/ricel123',
    color: '#75f1ff',
    svg_component: Twitter
  },
  {
    title: 'MyAnimeList',
    link: 'https://myanimelist.net/profile/Ricel123',
    color: '#2861d4',
    svg_component: MyAnimeList
  },
  {
    title: 'Jstris',
    link: 'https://jstris.jezevec10.com/u/RiceL123',
    color: '#ea6ef5',
    svg_component: Jstris
  },
  {
    title: 'Tetrio',
    link: 'https://ch.tetr.io/u/ricel123',
    color: '#e8a758',
    svg_component: Tetrio
  },
  {
    title: 'osu',
    link: 'https://osu.ppy.sh/users/16549400',
    color: '#ffbafc',
    svg_component: osu
  },
  {
    title: 'Spotify',
    link: 'https://open.spotify.com/user/75ugbigv9cpu446t1pctxw0rl?si=69cde5aae58142c5',
    color: '#43f071',
    svg_component: Spotify
  },
  {
    title: 'sheet',
    link: 'https://docs.google.com/spreadsheets/d/1_fq3KERt8A-90-qOTUsP87QtQFZgj6aZ-3efs_eJkMg/edit?usp=sharing',
    color: '#00b02f',
    svg_component: sheet
  },
  {
    title: 'Reddit',
    link: 'https://www.reddit.com/user/RiceL123/',
    color: '#f58936',
    svg_component: Reddit
  },
]);

let num = ref(0);

let goodDayMultiplier = Math.round(Math.random() * 1000000000);

onMounted(() => {
  let goodDaySpan = document.getElementById("goodDaySpan")
  goodDaySpan.style.fontSize = "20px";

  const incrementGoodDay = () => {
    const step = () => {
      if (num.value < goodDayMultiplier) {
        num.value += 1;

        if (num.value % 500 == 0) {
          goodDaySpan.style.fontSize = parseInt(goodDaySpan.style.fontSize) + 1 + "px";
        }
        requestAnimationFrame(step);
      }
    };
    requestAnimationFrame(step);
  };

  Array.from(document.getElementsByClassName("link")).forEach((x, index) => {
    const animation = x.animate(
      [
        { transform: "translate(0, 0) scale(1) rotate(0)", opacity: 1 }
      ],
      {
        duration: 1000,
        easing: "ease-out",
        iterations: 1,
        delay: index * 150,
      }
    );

    animation.persist();

    animation
      .finished
      .then(() => {
        x.style.transition = 'none'
        x.style.transform = 'translate(0, 0) scale(1) rotate(0)';
        x.style.opacity = "0.7";

        setTimeout(() => { x.style.removeProperty('transition') }, 0)
      });

    x.getElementsByTagName("svg")[0].animate(
      [
        { transform: "scale(3)" },
        { transform: "scale(1)" }
      ],
      {
        duration: 1500,
        easing: "ease-out",
        iterations: 1,
        delay: index * 150,
      }
    );
  });

  let textWrapper = document.querySelectorAll('.subline .letters');
  textWrapper.forEach(x => x.innerHTML = x.textContent.replace(/\S/g, "<span class='letter'>$&</span>"));

  let letters = document.querySelectorAll('.subline .letters .letter');

  letters.forEach((x, index) => {
    let delay = index < 33 ? index * 150 : (index + 4) * 150;
    x.animate(
      [
        { opacity: 0 },
        { opacity: 1 }
      ],
      { duration: 2000, delay, iterations: 'Infinity', easing: 'linear(0, .9, 1)' }
    );
  });


  incrementGoodDay();
});

</script>

<template>
  <Backdrop />

  <CursorTrail />

  <header style="display: flex; flex-direction: column; align-items: center;">
    <h1 style="font-size: 3rem;" class="chromatic-abberation">RiceL123
      Links</h1>


    <p class='subline' style="font-size: 1.2rem; color: white; text-shadow: black 2px 2px;">
      <span class="letters">hello. how are you? have a good x</span>
      <span id="goodDaySpan">{{ num }}</span>
      <span class="letters"> day</span>
    </p>
  </header>

  <div id="link-container">
    <WebLink v-for="(item, index) in items" :title="item.title" :link="item.link" :svg_color="item.color" :key="index">
      <component :is="item.svg_component" />
    </WebLink>
  </div>

</template>

<style scoped>
#link-container {
  display: flex;
  flex-direction: column;
  gap: 1em;
  max-width: 2000px;
  margin-inline: 3em;
  transition: all 0.5s
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

.chromatic-abberation {
  color: azure;
  text-shadow: rgba(255, 0, 0, 0.4) 10px 3px, rgba(0, 255, 255, 0.5) -3px 5px, rgba(255, 255, 0, 0.5) -3px -3px, rgba(255, 0, 255, 0.3) -10px 3px, black 3px 3px;
}

.subline .letter {
  display: inline-block;
  line-height: 1em;
}
</style>
