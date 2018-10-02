<template>
    <div class="block">
        <h2>Ты сегодня покормил кота?</h2>
        <div class="block-cats">

            <div v-bind:class="it.disabled ? 'disabled ct' : 'ct'" v-for="(it,i) in items" v-bind:key="i+it">
                <div :id="'item-'+i" class="item" @click="!it.disabled? selectPack($event, i): false">
                    <div class="trey"></div>
                    <div class="container">
                        <div class="info">
                            <div class="top-text">{{it["top-text"]}}</div>
                            <div class="title">
                                <p>Нямушка</p>
                                <p class="sub-title">{{it.title}}</p>
                            </div>
                            <div class="bottom-text">
                                <p v-for="(p,j) in it['bottom-text']" v-bind:key="p+j+i">
                                    {{p}}
                                </p>
                            </div>
                            <div class="main-img">
                                <img src="./../assets/images/cat.png" alt="">
                            </div>
                            <div class="round weight">
                                <p>{{it.weight}}</p>
                                <p>кг</p>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="buy-text" v-html="it['text-buy']"></div>
            </div>
        </div>
    </div>
</template>

<script>
    const info = require("./info")


    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        data() {
            return {
                items: info.items
            }
        },
        methods: {
            selectPack(ev, i) {
                const el = document.getElementById("item-" + i);
                el.classList.toggle("active");
            },

        },
        mounted() {
            document.querySelector(".buy-text .blue").onclick = function () {
                const el = this.parentElement.parentElement.querySelector(".item").classList.toggle("active");
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

    @font-face {
        font-family: Trebuchet;
        src: url("./../assets/fonts/Thin.otf");
    }

    html, body {
        height: 100%;
        margin: 0;
    }

    body {
        background: url("./../assets/images/bgr-main.png");
        background-size: 100%;
    }

    * {
        box-sizing: border-box;
        font-family: Trebuchet, serif;
        color: #666666;
        font-size: 16px;
        margin: 0;
        padding: 0;
    }

    .title, .title * {
        color: #000000;
        font-size: 48px;
        font-weight: bold;
    }

    %flex {
        -webkit-display: flex;
        -moz-display: flex;
        -ms-display: flex;
        -o-display: flex;
        -khtml-display: flex;
        display: flex;
    }

    @mixin jc($val) {
        -webkit-justify-content: $val;
        -moz-justify-content: $val;
        -ms-justify-content: $val;
        -o-justify-content: $val;
        -khtml-justify-content: $val;
        justify-content: $val;
    }

    @mixin ai($val) {
        -webkit-align-items: $val;
        -moz-align-items: $val;
        -ms-align-items: $val;
        -o-align-items: $val;
        -khtml-align-items: $val;
        align-items: $val;
    }

    @mixin fd($val) {
        -webkit-flex-direction: $val;
        -moz-flex-direction: $val;
        -ms-flex-direction: $val;
        -o-flex-direction: $val;
        -khtml-flex-direction: $val;
        flex-direction: $val;
    }

    .block {
        height: 100%;
        h2 {
            color: white;
            text-align: center;
            width: 100%;
            font-size: 36px;
            position: absolute;
            top: 10vh;
        }
    }

    .block-cats {
        @extend %flex;
        @include jc(space-around);
        @include ai(center);
        -webkit-flex-wrap: wrap;
        -moz-flex-wrap: wrap;
        -ms-flex-wrap: wrap;
        -o-flex-wrap: wrap;
        -khtml-flex-wrap: wrap;
        flex-wrap: wrap;
        height: 100%;
        .ct {
            position: relative;
            &:nth-child(2) .item, &:nth-child(2) .item:before, &:nth-child(2) .item:after, &:nth-child(2) .item .container .info .main-img {
                border-color: #d91667;
            }
            &:nth-child(2) .item .container .info .round {
                background: #d91667;
            }

            &:nth-child(3) .item, &:nth-child(3) .item:before, &:nth-child(3) .item:after, &:nth-child(3) .item .container .info .main-img {
                border-color: #b3b3b3;
            }

            &:nth-child(3) .item .container .info .round {
                background: #b3b3b3;
            }

            .item.active, .item.active:before, .item.active:after, .item.active .container .info .main-img {
                border-color: green;
            }

            .buy-text {
                color: #ffffff;
                font-size: 13px;
                font-weight: 400;
                line-height: 16px;
                text-align: center;
                margin-top: 15px;
                span.blue {
                    color: rgb(22, 152, 217);
                    cursor: pointer;
                }
                .yellow {
                    color: #ffff66;
                }
            }

            &.disabled {
                .item {
                    * {
                        opacity: 0.8;
                    }
                }
            }
        }

        .item {
            border-bottom: 4px solid #1698d9;
            width: 320px;
            height: 480px;
            border-radius: 0px 11px 11px 11px;
            /*text-align: center;*/
            overflow: hidden;
            position: relative;
            &:before {
                content: "";
                position: absolute;
                height: 100%;
                left: 0;
                top: -6px;
                width: 50px;
                border: solid #1698d9;
                border-width: 6px 0 0 4px;
                border-top-left-radius: 8px;
                -webkit-transform-origin: right bottom;
                transform-origin: right bottom;
                -webkit-transform: skewY(-45deg);
                transform: skewY(-45deg);
                z-index: -1;
                background-color: #f2f2f2;
            }
            &:after {
                position: absolute;
                content: '';
                top: 0;
                height: 100%;
                z-index: -1;
                left: 50px;
                width: calc(100% - 54px);
                border: 4px solid #1698d9;
                border-left: none;
                background-color: #f2f2f2;
            }
            .container {
                width: 100%;
                height: 100%;

                .info {
                    margin-left: 49px;
                    .top-text {
                        margin-top: 24px;
                    }
                    .title {
                        .sub-title {

                            font-size: 24px;
                        }
                    }
                    .bottom-text {
                        margin-top: 16px;
                        p {
                            font-size: 14px;
                        }
                    }

                    .round {
                        border-radius: 50%;
                        background: #1698d9;
                        width: 81px;
                        height: 81px;
                        &.weight {
                            @extend %flex;
                            @include jc(center);
                            @include ai(center);
                            @include fd(column);
                            position: absolute;
                            right: 15px;
                            bottom: 15px;
                            p {
                                color: white;
                                font-size: 42px;
                                line-height: 32px;
                                &:nth-child(2) {
                                    font-size: 24px;
                                }
                            }
                        }
                    }

                    .main-img {
                        border-left: 4px solid #1698d9;
                        position: absolute;
                        height: 100%;
                        width: 100%;
                        overflow: hidden;
                        top: 60px;
                        left: 0;
                        img {
                            position: absolute;
                            bottom: -35px;
                            left: -30px;
                        }
                    }
                }
            }

        }
    }

    @media screen and (max-height: 800px), screen and (max-width: 1000px){
        .block {
            h2 {
                position: static;
                margin-top: 20px;
                margin-bottom: 20px;
            }
        }
    }

</style>
