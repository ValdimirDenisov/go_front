<template>
    <v-container class="grey lighten-5">
        <v-row no-gutters class=" d-flex align-stretch"> 
          <v-col md="auto" class="d-flex">
            <v-card class="pa-2"  outlined tile>
              <slot> </slot>
            </v-card>
          </v-col>
          <v-col cols="10" md="5" class="d-flex" >
            <v-card class="pa-2 " style="width:300px;" outlined tile >
              Игроки
              <v-list subheader>
                <v-list-item v-for="player in players" :key="player">
                  <v-list-item-avatar>
                    <v-img :src="player.img"></v-img>
                  </v-list-item-avatar>
                  <v-list-item-content>
                    <v-list-item-title v-text="player.name"></v-list-item-title>
                  </v-list-item-content>
                  <v-list-item-avatar>
                    <v-img :src="player.color"></v-img>
                  </v-list-item-avatar>
                </v-list-item>
              </v-list>
              Управление игрой
              <v-slider v-model="value" step="1" thumb-label ticks></v-slider>
              <v-row no-gutters >
                <v-col>
                  <v-card class="pa-2" outlined tile>
                    <v-btn block color="primary" elevation="2" large>&lt;</v-btn>
                  </v-card>
                </v-col>
                <v-col>
                  <v-card class="pa-2" outlined tile>
                    <v-btn block color="primary" elevation="2" large>&gt;</v-btn>
                  </v-card>
                </v-col>
              </v-row>
              <template >
                  <v-card style="margin-top: 15px;">
                      <v-list two-line>
                        <template v-for="(item, index) in items.slice(0, 8)">
                          <v-subheader v-if="item.header" :key="item.header">
                            {{ item.header }}
                          </v-subheader>
                          <v-divider v-else-if="item.divider" :key="index"></v-divider>
                          <v-list-item v-else :key="item.title">
                            <v-list-item-content>
                              <v-list-item-title v-html="item.title"></v-list-item-title>
                              <v-list-item-subtitle v-html="item.subtitle"></v-list-item-subtitle>
                            </v-list-item-content>
                          </v-list-item>
                        </template>
                      </v-list>
                  </v-card>
              </template>


            </v-card>
          </v-col>
        </v-row>
      </v-container>
</template>

<script>
export default {
  name: 'viewGame',
  props: {
    
  },

  data: () => ({
    players: [{
      name: 'denisovV',
      img: 'https://games.mail.ru/hotbox/content_files/gallery/2020/12/11/d49a024e7ade40858a10df3b8976625d.png',
      color: 'https://pbs.twimg.com/ext_tw_video_thumb/1130497796958838784/pu/img/XZj79ABYvAjiQMJr.jpg'
    }, {
      name: 'XxJadxX',
      img: 'https://pbs.twimg.com/profile_images/1092700380222406656/wkhrxlhD.jpg',
      color: 'https://www.marmarland.com/2101/742.jpg'
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
