<template>
    <v-app>
        <v-main class="text-center ma-auto" style="width: 1000px">
			<TopTable :players="playerses" v-on:clickValue="getGame($event)" v-if="flag1"/>
            <viewGame :players="players" :items="items" :value="value" :max="max" v-on:changeValue="change($event)" v-if="flag">
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
            {header: 'Информация'},
            {title: 'Размер', subtitle: '13Х13'},
            {divider: true, inset: true},
            {title: 'Дата', subtitle: '28 марта 2021'},
            {divider: true, inset: true},
            {title: 'Результат', subtitle: '8.5'},
            {divider: true, inset: true},
            {title: 'Тип матча', subtitle: 'Рейтинговый'},
            {divider: true, inset: true},
        ],
        URL: 'http://127.0.0.1:8080/api/top'
    }),
    mounted() {
        this.axios.get(this.URL).then((response) => {
			this.playerses = response['data'] 
		})
    },
    methods: {
        change(a){
            this.value = a
			console.log(goBoard);
            this.$refs.board.updateBoard(this.value, this.move, this.size)
        },
		getGame(url) {
			this.flag = true
			this.flag1 = false
			let URL = 'http://127.0.0.1:8080/' + url;
			this.axios.get(URL).then((response) => {
				let d = response['data'];
				this.move = d['moves'];
				console.log(this.moves);
				this.size = +d['size'];
				this.max = d['moves'].length;
				this.items[1]['subtitle'] = d['size'] + 'X' + d['size'];
				this.items[3]['subtitle'] = d['date'];
				this.items[5]['subtitle'] = d['score'];
				this.items[7]['subtitle'] = d['gameType'];
				this.players[0] = {
					'name': d['players']['white']['name'] + ' ' + d['players']['white']['rank'],
					'img': d['players']['white']['avatar'],
					'color': 'https://pbs.twimg.com/ext_tw_video_thumb/1130497796958838784/pu/img/XZj79ABYvAjiQMJr.jpg',
					'alt': 'https://it.oplus.ru/uploads/gallery/user.png'
				}
				this.players[1] = {
					'name': d['players']['black']['name'] + ' ' + d['players']['black']['rank'],
					'img': d['players']['black']['avatar'],
					'color': 'https://www.marmarland.com/2101/742.jpg',
					'alt': 'https://it.oplus.ru/uploads/gallery/user.png'
				}
			});
		}
	}
};
</script>
