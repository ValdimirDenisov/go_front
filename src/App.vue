<template>
  <v-app>
    <v-main>
      <v-container class="grey lighten-5">
        <v-row no-gutters > 
          <v-col md="auto">
            <v-card class="pa-2" outlined tile>
              <goBoard :size="19" />
            </v-card>
          </v-col>
          <v-col cols="6" md="4">
            <v-card class="pa-2" outlined tile>
              Игроки
              <v-list subheader>
                <v-list-item v-for="player in players" :key="player">
                  <v-list-item-avatar>
                    <v-img :src="player.img"></v-img>
                  </v-list-item-avatar>
                  <v-list-item-content>
                    <v-list-item-title v-text="player.name"></v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
              </v-list>



              Управление игрой
              <v-slider v-model="value" step="1" thumb-label ticks></v-slider>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import goBoard from './components/goboard.vue'
export default {
  name: 'App',

  components: {
    goBoard
  },

  data: () => ({
    players: [{
      name: 'denisovV',
      img: 'https://games.mail.ru/hotbox/content_files/gallery/2020/12/11/d49a024e7ade40858a10df3b8976625d.png',
    }, {
      name: 'XxJadxX',
      img: 'https://pbs.twimg.com/profile_images/1092700380222406656/wkhrxlhD.jpg',
    }],
    value: 85,
  }),
};
</script>
