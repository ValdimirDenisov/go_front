<template>
    <v-app>
        <v-main class="text-center ma-auto" style="width: 1000px">
			<TopTable :players="playerses" v-on:clickValue="getGame($event)" v-if="flag1"/>
            <viewGame :players="players" :items="items" :value="value" :max="max" :time='move' v-on:changeValue="change($event)" v-on:goBack="changeFlags($event)" v-if="flag">
                <goBoard ref="board" :size="size" :value="value" :moves="move"/>
            </viewGame>
        </v-main>
    </v-app>
</template>

<script>
import goBoard from './components/goboard.vue'
import viewGame from './components/viewGame.vue'
import TopTable from './components/TopTable.vue'

export default {
    name: 'App',
    components: {
		TopTable,
        goBoard,
        viewGame,
    },

    data: () => ({
		flag: false,
		flag1: true,
        size: 19,
        players: [{}, {}],
		playerses: [],
        value: 0,
        max: 15,
		move: [],
        items: [
			{
				name: 'Информация',
				heigth: '13Х13',
				data: '28 марта 2021',
				result: 8.5,
				type: 'Рейтинговый',
				komi: 4.0,
				handicap: 0,
				time: '',
				rules: "Japanese",
			}
        ],
        URL: 'http://127.0.0.1:8080/api/top/'
    }),
    mounted() {
        this.axios.get(this.URL).then((response) => {
			this.playerses = response['data'] 
		})
    },
    methods: {
		changeFlags(x) {
			this.flag = false
			this.flag1 = x
		},
        change(a){
            this.value = a
            this.$refs.board.updateBoard(this.value, this.move, this.size)
        },
		getGame(url) {
			this.flag = true
			this.flag1 = false
			let URL = 'http://127.0.0.1:8080/' + url;
			this.axios.get(URL).then((response) => {
				let d = response['data'];
				this.move = d['moves'];
				this.size = +d['size'];
				this.max = d['moves'].length;
				this.items[0]['heigth'] = d['size'] + 'X' + d['size'];
				this.items[0]['data'] = d['date'];
				this.items[0]['result'] = d['score'];
				this.items[0]['type'] = d['gameType'];
				this.items[0]['handicap'] = d['handicap'];
				this.items[0]['time'] = d['time'];
				this.items[0]['komi'] = d['komi'];
				this.items[0]['rules'] = d['rules'];
				this.players[0] = {
					'name': d['players']['white']['name'] + '[' + d['players']['white']['rank'] + ']',
					'img': d['players']['white']['avatar'],
					'color': 'https://img.oboilux.ru/upload/iblock/bf0/bf0b666dd13a4fcec8ebc656d0bc48f1.jpg',
					'alt': 'https://it.oplus.ru/uploads/gallery/user.png',
					'time': d['time']
				}
				this.players[1] = {
					'name': d['players']['black']['name'] + '[' + d['players']['black']['rank'] + ']',
					'img': d['players']['black']['avatar'],
					'color': 'https://cdn.photosight.ru/sight/2006/06/05/1469552.jpg',
					'alt': 'https://it.oplus.ru/uploads/gallery/user.png',
					'time': d['time']
				}
			});
		}
	}
};
</script>
