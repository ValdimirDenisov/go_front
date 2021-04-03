<template>
    <div class="conteiner">
        <div class="table-conteiner9" v-if="size == 9">
            <div class="topline9">
                <div class="topline-item9" v-for="item in arrLetters9" :key="item">
                    {{ item }}
                </div>
            </div>
            <div class="second-table-conteiner9">
                <div class="left-line9">
                    <div class="left-line-item9" v-for="item in arrDigit9" :key="item">
                        {{ item }}
                    </div>
                </div>
                <div class="table9">
                    <div class="pole-conteiner9">
                        <div class="table-column9" v-for="item in (size - 1)" :key="item">
                            <div class="table-column-item9" v-for="item in (size - 1)" :key="item"></div>
                        </div>
                    </div>
                    <div class="game-container9">
                        <div class="table-column-play9" v-for="item in size" :key="item">
                            <div class="table-column-play-item9" v-for="item in size" :key="item">
                                <div class="item-target9"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>


        <div class="table-conteiner13" v-if="size == 13">
            <div class="topline13">
                <div class="topline-item13" v-for="item in arrLetters13" :key="item">
                    {{ item }}
                </div>
            </div>
            <div class="second-table-conteiner13">
                <div class="left-line13">
                    <div class="left-line-item13" v-for="item in arrDigit13" :key="item">
                        {{ item }}
                    </div>
                </div>
                <div class="table13">
                    <div class="pole-conteiner13">
                        <div class="table-column13" v-for="item in (size - 1)" :key="item">
                            <div class="table-column-item13" v-for="item in (size - 1)" :key="item"></div>
                        </div>
                    </div>
                    <div class="game-container13">
                        <div class="table-column-play13" v-for="item in size" :key="item">
                            <div class="table-column-play-item13" v-for="item in size" :key="item">
                                <div class="item-target13"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="table-conteiner19" v-if="size == 19">
            <div class="topline19">
                <div class="topline-item19" v-for="item in arrLetters19" :key="item">
                    {{ item }}
                </div>
            </div>
            <div class="second-table-conteiner19">
                <div class="left-line19">
                    <div class="left-line-item19" v-for="item in arrDigit19" :key="item">
                        {{ item }}
                    </div>
                </div>
                <div class="table19">
                    <div class="pole-conteiner19">
                        <div class="table-column19" v-for="item in (size - 1)" :key="item">
                            <div class="table-column-item19" v-for="item in (size - 1)" :key="item"></div>
                        </div>
                    </div>
                    <div class="game-container19">
                        <div class="table-column-play19" v-for="item in size" :key="item">
                            <div class="table-column-play-item19" v-for="item in size" :key="item">
                                <div class="item-target19"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>

<script>
export default {
    name: 'goBoard',
    props: {
        size: Number,
        value: Number,
        moves: Array,
    },
    mounted() {
        this.matrix = this.toMatrix(document.querySelectorAll('.table-column-play-item' + String(this.size)), this.size);
        // this.setButtons(this.matrix);
    }, data() {
        return {
            arrDigit9: ['9', '8', '7', '6', '5', '4', '3', '2', '1'],
            arrLetters9: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'J'],
            arrDigit13: ['13', '12', '11', '10', '9', '8', '7', '6', '5', '4', '3', '2', '1'],
            arrLetters13: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'J', 'K', 'L', 'M', 'N'],
            arrDigit19: ['19', '18', '17', '16', '15', '14', '13', '12', '11', '10', '9', '8', '7', '6', '5', '4', '3', '2', '1'],
            arrLetters19: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T'],
        }
    },
    methods: {
        get_color(i, j){
            if (this.matrix[i][j] === 123) return undefined
            let black_color_class = 'black-ball' + String(this.size);
            let white_color_class = 'white-ball' + String(this.size);
            if (this.matrix[i][j].classList.contains(black_color_class)) return 'black';
            else if (this.matrix[i][j].classList.contains(white_color_class)) return 'white';
            else return null
        },
        dfs_find(i, j) {
            if (this.visited[i][j] === 123) {
                this.dfs_flag = false;
                return;
            }
            this.visited[i][j] = 1;
            let current_color = this.get_color(i, j);
            for (let di = -1; di < 2; di++){
                for (let dj = -1; dj < 2; dj++) {
                    if (di !== 0 && dj !== 0) continue;
                    let color = this.get_color(i + di, j + dj);
                    if (color === null){
                        this.dfs_flag = false;
                        return;
                    }
                    if (this.visited[i + di][j + dj] === 0 && color === current_color) {
                        this.dfs_find(i + di, j + dj);
                    }
                }
            }
        },
        dfs_remove(i, j) {
            this.visited[i][j] = 1;
            let current_color = this.get_color(i, j);
            for (let di = -1; di < 2; di++){
                for (let dj = -1; dj < 2; dj++) {
                    if (di !== 0 && dj !== 0) continue;
                    let color = this.get_color(i + di, j + dj);
                    if (this.visited[i + di][j + dj] === 0 && color === current_color) {
                        this.dfs_remove(i + di, j + dj);
                    }
                }
            }
            if (current_color === 'black') {
                let black_color_class = 'black-ball' + String(this.size);
                this.matrix[i][j].classList.remove(black_color_class);
            } else {
                let white_color_class = 'white-ball' + String(this.size);
                this.matrix[i][j].classList.remove(white_color_class);
            }
        },
        checkNeighbour(i, j){
            this.visited = this.getVisited();
            this.dfs_flag = true;
            this.dfs_find(i, j);
            if (this.dfs_flag){
                this.visited = this.getVisited();
                this.dfs_remove(i, j);
            }
        },
        checkNeighbours(i, j){
            this.checkNeighbour(i - 1, j);
            this.checkNeighbour(i + 1, j);
            this.checkNeighbour(i, j - 1);
            this.checkNeighbour(i, j + 1);
        },
        getVisited() {
            let matrix = [];
            let mas = [];
            let inf = 123;
            for (let i = 0; i <= this.size + 1; i++) {
                mas.push(inf);
            }
            matrix.push(mas);
            mas = [];
            mas.push(inf);
            for (let i = 0; i < this.size * this.size; i++) {
                mas.push(0);
                if ((i + 1) % this.size == 0) {
                    mas.push(inf);
                    matrix.push(mas);
                    mas = [];
                    mas.push(inf);
                }
            }
            mas = [];
            for (let i = 0; i <= this.size + 1; i++) {
                mas.push(inf);
            }
            matrix.push(mas);
            return matrix;
        },
        toMatrix(res, size) {
            let matrix = [];
            let mas = [];
            let inf = 123;
            for (let i = 0; i <= size + 1; i++) {
                mas.push(inf);
            }
            matrix.push(mas);
            mas = [];
            mas.push(inf);
            for (let i = 0; i < res.length; i++) {
                mas.push(res[i]);
                if ((i + 1) % size == 0) {
                    mas.push(inf);
                    matrix.push(mas);
                    mas = [];
                    mas.push(inf);
                }
            }
            mas = [];
            for (let i = 0; i <= size + 1; i++) {
                mas.push(inf);
            }
            matrix.push(mas);
            return matrix;
        },
        setButtons(res) {
            let classes_black = 'black-ball' + String(this.size);
            let classes_white = 'white-ball' + String(this.size);
            let x = 1;
            let self = this;
            for (let i = 1; i <= this.size; i++) {
                for (let j = 1; j <= this.size; j++) {
                    //res[i][j].innerHTML = String(i);
                    res[i][j].addEventListener('click', function () {
                        if (!res[i][j].classList.contains(classes_black) && !res[i][j].classList.contains(classes_white)) {
                            if (x == 1) {
                                self.setPoint(res, i, j, classes_black);
                                x = x * -1;
                            } else {
                                self.setPoint(res, i, j, classes_white);
                                x = x * -1;
                            }
                        }
                    });
                }
            }
        },
        setPoint(res, i, j, color) {
            res[i][j].classList.add(color);
            this.checkNeighbours(i, j);
        },
        updateBoard(current_move, moves, size){
            let classes_black = 'black-ball' + String(size);
            let classes_white = 'white-ball' + String(size);
            for (let i = 1; i <= size; i++) {
                for (let j = 1; j <= size; j++) {
                    this.matrix[i][j].classList.remove(classes_black, classes_white);
                    this.matrix[i][j].children[0].classList.remove('opacityClass');
                }
            }
            let mas = moves
            for (let i = 0; i < current_move; i++) {
                if (mas[i]['color'] == 'black') {
                    this.setPoint(this.matrix, mas[i]['coords'][0], mas[i]['coords'][1], classes_black);
                    
                } else {
                    this.setPoint(this.matrix, mas[i]['coords'][0], mas[i]['coords'][1], classes_white);
                }
            }
            this.matrix[mas[current_move-1]['coords'][0]][mas[current_move-1]['coords'][1]].children[0].classList.add('opacityClass')
        }
    }
    

}
</script>

<style>
.opacityClass {
    opacity: 1 !important;
}
.conteiner {
    box-sizing: initial !important;
    text-align: left !important;
}

.table-conteiner19 {
    width: 630px;
    height: 630px;
    background-color: #333;
}

.topline19 {
    height: 30px;
    width: 630px;
    margin-left: 16px;
}

.topline-item19 {
    display: inline-block;
    vertical-align: top;
    text-align: center;
    padding-top: 7px;
    /* font-size: 10px; */
    width: 12px;
    height: 10px;
    margin-left: 20px;
    color: antiquewhite;
}

.left-line19 {
    display: inline-block;
    vertical-align: top;
    margin-top: 2px;
    width: 30px;
    height: 630px;
}

.left-line-item19 {
    height: 32px;
    width: 30px;
    text-align: center;
    color: antiquewhite;
}

.table19 {
    display: inline-block;
    vertical-align: top;
    width: 600px;
    height: 600px;
    background-color: #dfbd6d;
    padding: auto;
}

.table-column19 {
    width: 100%;
    height: 30px;
    margin-top: 2px;
}

.table-column-item19 {
    display: inline-block;
    vertical-align: top;
    height: 30px;
    width: 30px;
    border: 2px solid #333;
    margin-left: -2px;
}

.pole-conteiner19 {
    height: 650px;
    width: 650px;
    margin-left: 13px;
    padding-top: 9px;
}

.game-container19 {
    margin-top: -675px;
}

.table-column-play19 {
    height: 21px;
    margin-top: 11px;
}

.table-column-play-item19 {
    vertical-align: top;
    display: inline-block;
    width: 21px;
    height: 21px;
    margin-left: 10.98px;
    margin-top: 6px;
}

.table-column-play-item19:first-child {
    margin-left: 2px;
}

/* .table-column-play-item19:hover .item-target19 {
    opacity: 1;
} */

.black-ball19 {
    border-radius: 100%;
    background-color: #333;

}

.white-ball19 {
    border-radius: 100%;
    background-color: rgb(255, 232, 232);
}

.item-target19 {
    height: 10px;
    width: 10px;
    margin-left: 5.8px;
    margin-top: 5px;
    background-color: rgb(70, 218, 255);
    transition: 0.3s;
    opacity: 0;
}
</style>


<style>
.table-conteiner13 {
    width: 630px;
    height: 630px;
    background-color: #333;
}

.topline13 {
    height: 30px;
    width: 630px;
    margin-left: 16px;
}

.topline-item13 {
    display: inline-block;
    vertical-align: top;
    text-align: center;
    padding-top: 7px;
    /* font-size: 10px; */
    width: 25px;
    height: 10px;
    margin-left: 22px;
    color: antiquewhite;
}

.left-line13 {
    display: inline-block;
    vertical-align: top;
    margin-top: 9px;
    width: 30px;
    height: 630px;
}

.left-line-item13 {
    height: 47px;
    width: 30px;
    text-align: center;
    color: antiquewhite;
}

.table13 {
    display: inline-block;
    vertical-align: top;
    width: 600px;
    height: 600px;
    background-color: #dfbd6d;
    padding: auto;
}

.table-column13 {
    width: 100%;
    height: 45px;
    margin-top: 2px;
}

.table-column-item13 {
    display: inline-block;
    vertical-align: top;
    height: 45px;
    width: 45px;
    border: 2px solid #333;
    margin-left: -2px;
}

.pole-conteiner13 {
    height: 650px;
    width: 650px;
    margin-left: 18px;
    padding-top: 14px;
}

.game-container13 {
    margin-top: -680px;
}

.table-column-play13 {
    height: 36px;
    margin-top: 11px;
}

.table-column-play-item13 {
    vertical-align: top;
    display: inline-block;
    width: 36px;
    height: 36px;
    margin-left: 10.5px;
    margin-top: 6px;
}

.table-column-play-item13:first-child {
    margin-left: 2px;
}

/* .table-column-play-item13:hover .item-target13 {
    opacity: 1;
} */

.black-ball13 {
    border-radius: 100%;
    background-color: #333;

}

.white-ball13 {
    border-radius: 100%;
    background-color: rgb(255, 232, 232);
}

.item-target13 {
    height: 10px;
    width: 10px;
    margin-left: 13.3px;
    margin-top: 11px;
    background-color: rgb(70, 218, 255);
    transition: 0.3s;
    opacity: 0;
}
</style>


<style>
.table-conteiner9 {
    width: 600px;
    height: 600px;
    background-color: #333;
}

.topline9 {
    height: 42px;
    width: 558px;
    margin-left: 30px;
}

.topline-item9 {
    display: inline-block;
    vertical-align: top;
    text-align: center;
    padding-top: 12px;
    width: 31px;
    height: 42px;
    margin-left: 30px;
    color: antiquewhite;
}

.left-line9 {
    display: inline-block;
    vertical-align: top;
    margin-top: 29px;
    width: 42px;
    height: 558px;
}

.left-line-item9 {
    height: 61px;
    width: 42px;
    text-align: center;
    color: antiquewhite;
}

.table9 {
    display: inline-block;
    vertical-align: top;
    width: 558px;
    height: 558px;
    background-color: #dfbd6d;
    padding: auto;
}

.table-column9 {
    width: 100%;
    height: 60px;
    margin-top: 2px;
}

.table-column-item9 {
    display: inline-block;
    vertical-align: top;
    height: 60px;
    width: 60px;
    border: 2px solid #333;
    margin-left: -2px;
}

.pole-conteiner9 {
    height: 480px;
    width: 558px;
    margin-left: 30px;
    padding-top: 30px;
}

.game-container9 {
    margin-top: -510px;
}

.table-column-play9 {
    height: 62px;
}

.table-column-play-item9 {
    vertical-align: top;
    display: inline-block;
    width: 50px;
    height: 50px;
    margin: 3px;
    margin-left: 8px;
    margin-top: 5px;
}

.table-column-play-item9 :first-child {
    margin-left: 8px;
}

/* .table-column-play-item9:hover .item-target9 {
    opacity: 1;
} */

.black-ball9 {
    border-radius: 100%;
    background-color: #333;

}

.white-ball9 {
    border-radius: 100%;
    background-color: rgb(255, 232, 232);
    width: 50px;
    height: 50px;
    margin: 3px;
    margin-left: 8px;
    margin-top: 5px;
}

.item-target9 {
    height: 30px;
    width: 30px;
    margin: 10px;
    background-color: rgb(70, 218, 255);
    transition: 0.3s;
    opacity: 0;
}
</style>
