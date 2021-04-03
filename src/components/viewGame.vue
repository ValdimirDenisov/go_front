<template>
    <v-container style="width: 1140px" class="">
        <v-row no-gutters class=" d-flex align-stretch"> 
          <v-col md="auto" class="d-flex">
            <v-card class="pa-2"  outlined tile>
              <slot> </slot>
            </v-card>
          </v-col>
          <v-col cols="13" md="5" class="d-flex" >
            <v-card class="pa-2 " style="width:380px;" outlined tile >
              Игроки
              <v-list subheader>
                <v-list-item v-for="player in players" :key="player">
                  <v-list-item-avatar>
                    <v-img :lazy-src="player.alt" :src="player.img"></v-img>
                  </v-list-item-avatar>
                  <v-list-item-content>
                    <v-list-item-title v-text="player.name+' (' + player.time +')'"></v-list-item-title>
                  </v-list-item-content>
                  <v-list-item-avatar>
                    <v-img :src="player.color"></v-img>
                  </v-list-item-avatar>
                </v-list-item>
              </v-list>
              Управление игрой
              <v-slider v-model="value" :max="max" step="1" thumb-label @change="update_slider()"></v-slider>
              <v-row no-gutters >
                <v-col>
                  <v-card class="pa-2" outlined tile>
					<v-btn block color="primary" elevation="2" large @click="value = value - 1;update_slider()" v-if="value > 0">&lt;</v-btn>
                    <v-btn block color="primary" elevation="2" large @click="value = value - 1;update_slider()" disabled v-if="value === 0">&lt;</v-btn>
                  </v-card>
                </v-col>
                <v-col>
                  <v-card class="pa-2" outlined tile>
                    <v-btn block color="primary" elevation="2" large @click="value = value + 1;update_slider()" v-if="value < max">&gt;</v-btn>
                    <v-btn block color="primary" elevation="2" large @click="value = value + 1;update_slider()" disabled v-if="value === max">&gt;</v-btn>
                  </v-card>
                </v-col>
              </v-row>
              <template >
				<v-container fluid>
					<v-data-iterator :items="items" :items-per-page.sync="itemsPerPage" hide-default-footer>
						<template v-slot:default="props">
							<v-row>
								<v-col v-for="item in props.items" :key="item.name">
									<v-card>
										<v-card-title class="subheading font-weight-bold">
											{{ item.name }}
										</v-card-title>
										<v-divider></v-divider>
										<v-list dense>
											<v-list-item style="margin-top: -12px">
												<v-list-item-content>Размер:</v-list-item-content>
												<v-list-item-content class="align-end">
													{{ item.heigth }}
												</v-list-item-content>
											</v-list-item>	
											
											<v-list-item style="margin-top: -12px">
												<v-list-item-content>Дата:</v-list-item-content>
												<v-list-item-content class="align-end">
													{{ item.data }}
												</v-list-item-content>
											</v-list-item>	
											
											
											<v-list-item style="margin-top: -12px">
												<v-list-item-content>Результат:</v-list-item-content>
												<v-list-item-content class="align-end">
													{{ item.result }}
												</v-list-item-content>
											</v-list-item>	

											
											<v-list-item style="margin-top: -12px">
												<v-list-item-content>Тип матча:</v-list-item-content>
												<v-list-item-content class="align-end">
													{{ item.type }}
												</v-list-item-content>
											</v-list-item>	

											<v-list-item style="margin-top: -12px">
												<v-list-item-content>Handicap:</v-list-item-content>
												<v-list-item-content class="align-end">
													{{ item.handicap }}
												</v-list-item-content>
											</v-list-item>

											<v-list-item style="margin-top: -12px">
												<v-list-item-content>Коми:</v-list-item-content>
												<v-list-item-content class="align-end">
													{{ item.komi }}
												</v-list-item-content>
											</v-list-item>

											<v-list-item style="margin-top: -12px">
												<v-list-item-content>Правила:</v-list-item-content>
												<v-list-item-content class="align-end">
													{{ item.rules }}
												</v-list-item-content>
											</v-list-item>
										</v-list>
									</v-card>
								</v-col>
							</v-row>
						</template>
					</v-data-iterator>
				</v-container>
              </template>
				<v-btn block color="primary" elevation="2" @click="goBack()">Назад</v-btn>
            </v-card>
          </v-col>
        </v-row>
    </v-container>
</template>

<script>
	export default {
		name: 'viewGame',
		props: ['players', 'items', 'value', 'max', "time"],
		data: () => ({
			itemsPerPage: 1,

		}),
		methods: {
			update_slider() {
				if (this.time[this.value].color === 'white') {
					this.players[0].time = this.time[this.value].time;
                    let prevMove = this.value;
                    while (prevMove >= 0 && this.time[prevMove].color !== 'black') {
						prevMove--;
                    }
                    if (prevMove === -1) this.players[1].time = this.items[0]['time']
					else this.players[1].time = this.time[this.value].time;
				} else {
					this.players[1].time = this.time[this.value].time;
					let prevMove = this.value;
					while (prevMove >= 0 && this.time[prevMove].color !== 'white') {
						prevMove--;
					}
					if (prevMove === -1) this.players[0].time = this.items[0]['time']
					else this.players[0].time = this.time[this.value].time;
				}
				this.$emit('changeValue', this.value)
			},
			goBack() {
				this.$emit('goBack', true)
			}
		}
	};
</script>

<style>
.v-image__image--preload{
    filter: unset !important;
}
</style>