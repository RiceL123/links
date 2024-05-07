<script setup>
import WebLink from './components/WebLink.vue'
import { ref } from 'vue'

const items = ref([
  {
    title: 'Websit',
    link: 'https://ricel123.netlify.app/',
    logo: 'https://files.catbox.moe/oi37kr.png'
  },
  {
    title: 'Youtube',
    link: 'https://www.youtube.com/@RiceL123',
    logo: '/yt.svg'
  },
  {
    title: 'Github',
    link: 'https://github.com/ricel123',
    logo: '/github.svg'
  },
  {
    title: 'Twitch',
    link: 'https://www.twitch.tv/ricel12345',
    logo: '/twitch.svg'
  },
  {
    title: 'Instagram',
    link: 'https://www.instagram.com/ricel12345/',
    logo: '/insta.svg'
  },
  {
    title: 'Twitter',
    link: 'https://twitter.com/ricel123',
    logo: '/twitter.svg'
  },
  {
    title: 'My AnimeList',
    link: 'https://myanimelist.net/profile/Ricel123',
    logo: '/anime.svg'
  },
  {
    title: 'Jstris',
    link: 'https://jstris.jezevec10.com/u/RiceL123',
    logo: '/jstris.svg'
  },
  {
    title: 'tetrio',
    link: 'https://ch.tetr.io/u/ricel123',
    logo: '/tetrio.svg'
  },
  {
    title: 'osu',
    link: 'https://osu.ppy.sh/users/16549400',
    logo: '/osu.svg'
  },
  {
    title: 'spotify',
    link: 'https://open.spotify.com/user/75ugbigv9cpu446t1pctxw0rl?si=69cde5aae58142c5',
    logo: '/spotify.svg'
  },
  {
    title: 'sheet',
    link: 'https://docs.google.com/spreadsheets/d/1_fq3KERt8A-90-qOTUsP87QtQFZgj6aZ-3efs_eJkMg/edit?usp=sharing',
    logo: '/sheet.svg'
  },
  {
    title: 'reddit',
    link: 'https://www.reddit.com/user/RiceL123/',
    logo: '/reddit.svg'
  },

])
</script>

<template>
  <header>
    <h2>Links for RiceL123</h2>
  </header>

  <div id="link-container">
    <WebLink 
    v-for="item in items"
    :title="item.title"
    :link="item.link"
    :logo="item.logo"
  ></WebLink>
  </div>

  <p style="position: absolute; place-self: end; padding-right: 1rem; font-size: smaller;">background art by me 💀</p>
</template>

<style scoped>


#link-container {
  gap: 2em;
  display: grid;
    grid-template-areas:
        "main main . main main"
        "main main . main main"
        "main main main main main";
    grid-template-columns: repeat(5, 1fr);
    grid-auto-rows: minmax(100px, auto);
}
</style>