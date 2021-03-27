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
              Управление игрой
              <v-slider v-model="value" step="10" thumb-label ticks></v-slider>
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
    //
  }),
};
</script>
