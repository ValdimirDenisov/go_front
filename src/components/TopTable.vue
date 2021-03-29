<template>
    
    <v-row no-gutters class="text-center"> 
        <v-col >
            <v-card>
                Топ 100 игроков
                <v-data-table :headers="headers" :items="players" :items-per-page="10" class="elevation-1">
                    <template v-slot:item.urls[0]="{ item }">
                        <v-btn color="primary" elevation="2" v-on:click="clickButton(item.urls[0])"> Клик </v-btn>
                    </template>
                    <template v-slot:item.urls[1]="{ item }">
                        <v-btn color="primary" elevation="2" v-on:click="clickButton(item.urls[1])"> Клик </v-btn>
                    </template>
                </v-data-table>
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
    export default {
        name: 'TopTable',
        props: ['players'],
        data () {
            return {
                headers: [
                { text: 'Игрок', align: 'start', sortable: false, value: 'name' },
                { text: 'Рейтинг', value: 'rank' },
                { text: 'Место', value: 'position' },
                { text: 'Последняя игра', value: 'urls[0]' },
                { text: 'Предпоследняя игра', value: 'urls[1]' }],
            }
        },
        methods: {
            clickButton(href) {
                this.$emit('clickValue', href)
            }
        }
    }
</script>

<style>

</style>