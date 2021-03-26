<template> 
    <div class="conteiner">
        <div class="table-conteiner9" v-if="size == 9">
            <div class="topline9">
                <div class="topline-item9" v-for="item in arrLetters9">
                    {{item}}
                </div>
            </div>
            <div class="second-table-conteiner9">
                <div class="left-line9">
                    <div class="left-line-item9" v-for="item in arrDigit9">
                        {{item}}
                    </div>
                </div>
                <div class="table9">
                    <div class="pole-conteiner9">
                        <div class="table-column9" v-for="item in (size - 1)">
                            <div class="table-column-item9" v-for="item in (size - 1)"></div>
                        </div>
                    </div>
                    <div class="game-container9">
                        <div class="table-column-play9" v-for="item in size">
                            <div class="table-column-play-item9" v-for="item in size">
                                <div class="item-target9"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        
        <div class="table-conteiner13" v-if="size == 13">
            <div class="topline13">
                <div class="topline-item13" v-for="item in arrLetters13">
                    {{item}}
                </div>
            </div>
            <div class="second-table-conteiner13">
                <div class="left-line13">
                    <div class="left-line-item13" v-for="item in arrDigit13">
                        {{item}}
                    </div>
                </div>
                <div class="table13">
                    <div class="pole-conteiner13">
                        <div class="table-column13" v-for="item in (size - 1)">
                            <div class="table-column-item13" v-for="item in (size - 1)"></div>
                        </div>
                    </div>
                    <div class="game-container13">
                        <div class="table-column-play13" v-for="item in size">
                            <div class="table-column-play-item13" v-for="item in size">
                                <div class="item-target13"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="table-conteiner19" v-if="size == 19">
            <div class="topline19">
                <div class="topline-item19" v-for="item in arrLetters19">
                    {{item}}
                </div>
            </div>
            <div class="second-table-conteiner19">
                <div class="left-line19">
                    <div class="left-line-item19" v-for="item in arrDigit19">
                        {{item}}
                    </div>
                </div>
                <div class="table19">
                    <div class="pole-conteiner19">
                        <div class="table-column19" v-for="item in (size - 1)">
                            <div class="table-column-item19" v-for="item in (size - 1)"></div>
                        </div>
                    </div>
                    <div class="game-container19">
                        <div class="table-column-play19" v-for="item in size">
                            <div class="table-column-play-item19" v-for="item in size">
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
            size: Number
        }, 
        mounted() {
            let classes = 'black-ball' + String(this.size);
            let res = document.querySelectorAll('.table-column-play-item' + String(this.size));
            for (let i = 0; i < res.length; i++) {
                res[i].addEventListener('click', function() {
                    res[i].classList.add(classes);
                });
            }
        }, data() {
            return {
                arrDigit9: ['9', '8', '7', '6', '5', '4', '3', '2', '1'],
                arrLetters9: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'J'],
                arrDigit13: ['13', '12', '11', '10', '9', '8', '7', '6', '5', '4', '3', '2', '1'],
                arrLetters13: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'J', 'K', 'L', 'M', 'N'],
                arrDigit19: ['19', '18', '17', '16', '15', '14','13', '12', '11', '10', '9', '8', '7', '6', '5', '4', '3', '2', '1'],
                arrLetters19: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T'],
            }
        }
        
    }
</script>

<style>
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

    .table-column-play-item19:hover .item-target19{
        opacity: 1;
    }

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

    .table-column-play-item13:hover .item-target13{
        opacity: 1;
    }

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

    .table-column-play-item9:hover .item-target9{
        opacity: 1;
    }

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