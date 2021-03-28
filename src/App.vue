<template>
  <v-app>
    <v-main>
      <viewGame> 
        <goBoard :size="19" />
      </viewGame>
    </v-main>
  </v-app>
</template>

<script>
import goBoard from './components/goboard.vue'
import viewGame from './components/viewGame.vue'
export default {
  name: 'App',
  components: {
    goBoard,
    viewGame,
  },

  data: () => ({
    players: [{
      name: 'denisovV',
      img: 'https://games.mail.ru/hotbox/content_files/gallery/2020/12/11/d49a024e7ade40858a10df3b8976625d.png',
      color: 'https://pbs.twimg.com/ext_tw_video_thumb/1130497796958838784/pu/img/XZj79ABYvAjiQMJr.jpg'
    }, {
      name: 'XxJadxX',
      img: 'https://pbs.twimg.com/profile_images/1092700380222406656/wkhrxlhD.jpg',
<<<<<<< HEAD
      color: 'https://tools-profi.ru/upload/iblock/2da/2da16b51b08195c8988a13487cbf9d04.jpg'
=======
      color: 'https://www.marmarland.com/2101/742.jpg'
>>>>>>> 6afc009cabac37e343a09c66cad8d3a39e6ce047
    }],
    value: 85,
    items: [
        { header: 'Информация' },
        { title: 'Размер', subtitle: '13Х13' },
        { divider: true, inset: true },
        { title: 'Дата', subtitle: '28 марта 2021' },
        { divider: true, inset: true },
        { title: 'Komi', subtitle: '8.5' },  
        { divider: true, inset: true },
        { title: 'Тип матча', subtitle: 'Рейтинговый' }, 
        { divider: true, inset: true },
    ],
  }),
};
</script>
