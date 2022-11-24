<template>
    <div id="app">
        <div class="header">
            <div class="first_section">
                <div class="logo">
                    HUMY
                </div>
                <div class="menu">
                    <div class="menu__item" v-for="item in menuItems" :key="item">
                        {{ item }}
                    </div>
                </div>
                <div class="search">
                    <img src="./assets/MagnifyingGlass.png" alt="MagnifyingGlass">
                </div>
            </div>
            <div class="second_section">
                Book Now
            </div>
        </div>

        <div class="content">
            <div class="first_section">
                <div class="play_btn">
                    <img src="./assets/play.png" alt="play">
                </div>
                <div class="top_btn">
                    <div class="california">CALIFORNIA, USA</div>
                </div>
                <div class="top_btn">
                    <div class="house">HOUSE</div>
                </div>
                <div class="price">
                    <div class="text">Price</div>
                    <div class="number">$23000</div>
                </div>
                <div class="details">
                    <div>DETAILS</div>
                </div>
                <div class="bar" @mousemove="triggerBar($event)">
                    <div class="bigBar" :style="barX"></div>
                </div>
            </div>

            <div class="second_section">
                <div class="text">
                    <div>find the best property for you</div>
                    <img class="star"
                        v-for="i in 3" :key="i"
                        src="./assets/Star.png" alt="star"
                    >
                </div>

                <div class="description">
                    <div class="description__text">
                        We will help you to find the <b>best property</b> with the best offer arround the <b>World</b>
                    </div>
                    <div class="icon">
                        <img src="./assets/Globe.png" alt="Globe">
                    </div>
                </div>
                
                <div class="btn_find">
                    <div class="btn">
                        Let's Find
                        <img src="./assets/arrow_find.png" alt="arrow">
                    </div>
                </div>
            </div>
        </div>

        <div class="footer">
            <div class="santa">
                <div class="sale">Sale Up to</div>
                <div class="number">20%</div>
                <div class="christmas">Special Christmas</div>
            </div>
            <div class="footer__menu">
                <div class="item"
                    :class="{'active': item.isActive}"
                    @click="changeFooterItem(index)"
                    v-for="(item, index) in footerItems" :key="item.text"
                >
                    {{ item.text }}
                    <img src="./assets/arrow_footer.png" alt="arrow">
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'App',

    data() {
        return {
            menuItems: [
                "Buy",
                "Sell",
                "Maps",
                "About Us",
                "Contact Us"
            ],

            footerItems: [
                {
                    text: "Home",
                    isActive: false,
                },
                {
                    text: "Apartment",
                    isActive: true,
                },
                {
                    text: "Rent",
                    isActive: false,
                },
                {
                    text: "Other",
                    isActive: false,
                },
            ],
            x: 0,
        }
    },

    computed: {
        barX() {
            const bigBarElement = document.querySelector('.bigBar')
            const bigBarWidth = bigBarElement.offsetWidth

            const barElement = document.querySelector('.bar')
            const barWidth = barElement.offsetWidth

            if(this.x < (bigBarWidth / 2)) return `transform: translate(0%, -50%)`
            else if (this.x > (barWidth - bigBarWidth / 2)) return `transform: translate(${(barWidth - bigBarWidth)}px, -50%)`
            return `transform: translate(calc(${this.x}px - 50%), -50%)`
        }
    },

    methods: {
        changeFooterItem(index) {
            const previousIndex = this.footerItems.map(item => item.isActive).indexOf(true)
            this.footerItems[previousIndex].isActive = false
            this.footerItems[index].isActive = true
        },

        triggerBar(e) {
            const xClient = e.clientX
            const padding = 40
            this.x = xClient - padding
        }
    },
}
</script>

<style lang="scss">
// COLORS
$orange: #FC7B53;
$black: #0A0909;
$white: #FFFDFA;
$green: #D7FFC5;
$purple: #DBACFF;
$yellow: #FEC477;
$pink: #FFBDD5;

// POLICE
@font-face {
    font-family: 'Poppins_SemiBold';
    src: url("./assets/police/Poppins-SemiBold.ttf");
}

@font-face {
    font-family: 'Poppins_Regular';
    src: url("./assets/police/Poppins-Regular.ttf");
}

@font-face {
    font-family: 'BebasNeue_Regular';
    src: url("./assets/police/BebasNeue-Regular.ttf");
}

body {
    margin: 0;
    background: black;
    box-sizing: border-box;
    overflow: hidden;
}

.header {
    display: flex;
    width: 100vw;
    height: 8vh;

    .first_section,
    .second_section {
        display: flex;
        align-items: center;

        border: 1px solid $black;
        border-radius: 20px;
    }

    .first_section {
        flex: 1;
        width: calc(85% - 80px);
        padding-inline: 40px;

        background: white;

        .logo {
            font-size: 32px;
            font-family: 'BebasNeue_Regular';
            flex: 1;

            cursor: pointer;
        }

        .menu {
            display: flex;
            gap: 40px;
            margin-inline: 25%;
            flex: 4;

            font-family: 'Poppins_Regular';
            font-size: 16px;
            white-space: nowrap;

            &__item {
                cursor: pointer;

                &:hover {
                    color: $purple;
                    transform: scale(1.05);
                    transition: all 250ms ease;
                }

                &:not(:hover) {
                    color: #000;
                    transform: scale(1);
                    transition: all 250ms ease;
                }
            }
        }

        .search {
            flex: 1;
            display: flex;
            justify-content: flex-end;

            cursor: pointer;
        }
    }

    .second_section {
        width: 15%;
        justify-content: center;

        background: $orange;
        font-family: 'Poppins_SemiBold';
        font-size: 20px;
        cursor: pointer;

        &:hover {
            font-size: 24px;
            transition: all 250ms ease;
        }

        &:not(:hover) {
            font-size: 20px;
            transition: all 250ms ease;
        }
    }
}

.content {
    width: 100vw;
    height: 70vh;
    display: flex;

    .first_section,
    .second_section {
        height: 100%;
    }

    .first_section {
        width: 65%;
        height: calc(100% - 80px);
        padding: 40px;
        position: relative;

        background: url('./assets/background_video.png') $white;
        background-size: cover;
        border: 1px solid $black;
        border-radius: 20px;

        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;

        .play_btn {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);

            display: flex;
            align-items: center;
            justify-content: center;

            width: 78px;
            height: 78px;

            background: $yellow;
            border: 1px solid $black;
            box-shadow: 6px 6px 0px #000000;
            border-radius: 20px;
            cursor: pointer;

            &:hover {
                img {
                    transform: scale(1.15);
                    transition: transform 250ms ease;
                }
            }

            &:not(:hover) {
                img {
                    transform: scale(1);
                    transition: transform 250ms ease;
                }
            }
        }

        .price,
        .details {
            width: 50%;
            height: calc(49% - 20px);
            padding-bottom: 20px;
        }

        .top_btn {
            width: 50%;
            height: 49%;

            & :nth-child(n) {
                width: fit-content;
                height: fit-content;
                padding: 6px 14px;

                border: 1px solid #0A0909;
                box-shadow: 6px 6px 0px #000000;
                border-radius: 20px;
                font-family: "BebasNeue_Regular";
                cursor: pointer;
            }

            &:nth-child(3) {
                display: flex;
                justify-content: flex-end;
            }

            .california {
                background: $green;
            }

            .house {
                background: $purple;
            }
        }

        .price {
            display: flex;
            flex-direction: column;
            justify-content: flex-end;

            .text {
                font-size: 14px;
                font-family: 'Poppins_Regular';
            }

            .number {
                color: $yellow;
                font-size: 64px;
                font-family: 'BebasNeue_Regular';
                -webkit-text-stroke: 1px #000;
                text-shadow: 4px 4px 0px #000;
            }
        }

        .details {
            display: flex;
            justify-content: flex-end;
            align-items: flex-end;

            div {
                transform: translateY(-10px);
                padding: 12px 44px;

                background: #FFFFFF;
                border: 1px solid #0A0909;
                box-shadow: 6px 6px 0px #000000;
                border-radius: 20px;

                font-size: 20px;
                font-family: 'Poppins_SemiBold';
                cursor: pointer;
            }
        }

        // Hover effect
        .top_btn,
        .details {
            div:hover {
                transform: rotate(2deg);
                transition: transform 1s ease;
            }

            div:not(:hover) {
                transform: rotate(0deg);
                transition: transform 1s ease;
            }
        }

        .bar {
            width: 100%;
            height: 2%;
            position: relative;

            &:before, .bigBar {
                position: absolute;
                top: 50%;
                transform: translateY(-50%);
                background: #000;
            }

            &:before {
                content:'';
                width: 100%;
                height: 1px;
            }

            .bigBar {
                width: 25%;
                height: 5px;
                border-radius: 20px;
            }
        }
    }

    .second_section {
        width: 35%;
        display: flex;
        flex-direction: column;

        .text {
            height: calc(60% - 80px);
            padding: 40px;

            background: $white;
            border: 1px solid $black;
            border-radius: 20px;

            font-size: 96px;
            font-family: 'BebasNeue_Regular';
            text-transform: uppercase;

            div {
                width: 70%;
                line-height: 90px;
            }

            .star {
                width: fit-content;
                height: fit-content;

                position: absolute;

                &:nth-of-type(1) {
                    top: 14%;
                    right: 40px;
                }

                &:nth-of-type(2) {
                    width: 26px;
                    height: 26px;

                    top: 23%;
                    right: 110px;
                }

                &:nth-of-type(3) {
                    width: 31px;
                    height: 31px;

                    top: 35.5%;
                    right: 60px;
                }
            }
        }

        .description {
            display: flex;
            width: 100%;
            height: 20%;

            &__text {
                width: calc(70% - 70px);
                padding: 40px 35px;

                background: $white;
                border: 1px solid $black;
                border-radius: 20px;

                font-family: 'Poppins_Regular';
            }

            .icon {
                width: 30%;
                // padding: 15px;

                display: flex;
                align-items: center;
                justify-content: center;

                background: $green;
                border: 1px solid $black;
                border-radius: 20px;

                img {
                    transform: rotate(15deg);
                }
            }

        }

        .btn_find {
            width: 100%;
            height: 20%;

            display: flex;
            align-items: center;

            .btn {
                width: 100%;
                height: 60%;
                transform: rotate(5.78deg);

                display: flex;
                align-items: center;
                justify-content: center;
                gap: 10px;

                background: $orange;
                border-radius: 20px;

                font-family: 'Poppins_SemiBold';
                font-size: 20px;
                cursor: pointer;

                &:hover {
                    img {
                        transform: translateX(100%);
                        transition: transform 250ms ease;
                    }
                }

                &:not(:hover) {
                    img {
                        transform: translateX(0%);
                        transition: transform 250ms ease;
                    }
                }
            }
        }
    }
}

.footer {
    width: 100vw;
    height: 22vh;

    display: flex;

    .santa {
        width: calc(26% - 80px);
        height: calc(100% - 60px);
        padding: 30px 40px;
        
        background-color: $pink;
        background-image: url('./assets/santa_head.png');
        background-size: contain;
        background-position-x: right;
        background-repeat: no-repeat;

        border: 1px solid $black;
        border-radius: 20px;

        .sale {
            width: 50%;
            font-size: 24px;
            font-family: 'Poppins_SemiBold';

        }

        .number {
            height: 100px;
            transform: translateY(-20px);

            font-size: 120px;
            font-family: 'BebasNeue_Regular';
        }

        .christmas {
            transform: translateY(10px);
            font-family: 'Poppins_Regular';

        }
    }

    &__menu {
        width: calc(74% - 80px);
        height: calc(100% - 80px);
        padding: 40px;

        display: flex;
        gap: 20px;

        background: $white;
        border: 1px solid #0A0909;
        border-radius: 20px;

        .item {
            width: 25%;
            padding: 25px;

            display: flex;
            flex-direction: column;
            justify-content: space-between;

            background: $white;
            border: 1px solid $black;
            box-shadow: 4px 4px 0px #000;
            border-radius: 20px;

            font-size: 40px;
            font-family: 'BebasNeue_Regular';
            cursor: pointer;

            &.active {
                background: $purple !important;
                box-shadow: 12px 12px 0px #000 !important;
                transform: rotate(-6.65deg) !important;
            }

            &:hover {
                background: $purple;
                box-shadow: 12px 12px 0px #000;
                transform: rotate(-6.65deg);
                transition: all 250ms ease;
            }

            &:not(:hover) {
                background: $white;
                box-shadow: 4px 4px 0px #000;
                transform: rotate(0deg);
                transition: all 250ms ease;
            }

            img {
                align-self: flex-end;
            }
        }
    }
}
</style>
