<template>
    <v-app>
        <v-main>
            <viewGame :players="players" :items="items" :value="value" :max="max" v-on:changeValue="change($event)">
                <goBoard :size="19" :value="value"/>
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
        size: 19,
        players: [{}, {}],
        value: 0,
        max: 15,
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
        URL: 'http://127.0.0.1:8080/api/game?player=RaksaRami&game_id=0'
    }),
    mounted() {
        this.axios.get(this.URL).then((response) => {
            console.log(response['data']);
            let d = response['data'];
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
    },
    methods: {
        change(a){
            this.value = a
            goBoard.methods.updateBoard(this.value)
        }
    }

};
</script>
