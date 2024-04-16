<template>
    <div class="card" @mouseover="cardInfoToggle(true)" @mouseleave="cardInfoToggle(false)">
        <div class="card_info" v-show="cardInfo" >
            <p><span class="card_title">Titolo: </span>{{ title }}</p>
            <p><span class="card_ogtitle">Titolo og: </span> {{ originalTitle }}</p>
            <p class="card_language">
                <span class="card_vote">Lingua: </span>{{ element.original_language }} 
                <img v-if="element.original_language === 'it'" width="30" height="30" src="https://img.icons8.com/emoji/48/italy-emoji.png" alt=""/>
                <img v-if="element.original_language === 'fr'" width="30" height="30" src="https://img.icons8.com/emoji/48/france-emoji.png" alt=""/>
                <img v-if="element.original_language === 'en'" width="30" height="30" src="https://img.icons8.com/emoji/48/us-outlying-islands-emoji.png" alt=""/>
                <img v-if="element.original_language === 'ja'" width="30" height="30" src="https://img.icons8.com/color/48/japan.png" alt="japan"/>
            </p>
            <p><span class="card_vote">Voto: </span><font-awesome-icon v-for="i in 5" :class="i <= starConverter(element.vote_average) ? 'star':''" icon="star"/></p>
        </div>
        <img class="card_poster" :src="`https://image.tmdb.org/t/p/w154/${element.poster_path}`" alt="">
    </div>
</template>

<script>

import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { library } from '@fortawesome/fontawesome-svg-core'
import { faStar } from '@fortawesome/free-solid-svg-icons'
import { longArrowRight } from 'fontawesome'
// import { faSearch } from '@fortawesome/free-solid-svg-icons'

library.add(faStar)
// library.add(faSearch)

export default {
    props : ['element','title','originalTitle'],

    data() {
        return{
            cardInfo: false
        }
    },

    components:{
        FontAwesomeIcon
    },

    methods: {
        starConverter(vote) {
            const score =  Math.floor(vote / 2)
            return score
        },

        cardInfoToggle(status) {
            this.cardInfo = status
            console.log(this.cardInfo);
        }
    }
}
</script>

<style lang="scss" scoped>

.card {
    border: 3px solid transparent;
    width: 250px;
    height: 400px;
    margin: 2px;
    position: relative;

    &:hover{
        cursor: pointer;
        border: 3px solid red;
    }
}

.card_info{
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    gap: 20px;
    padding: 35px;
    background-color: rgba( #1B1B1B,0.8);
    position: absolute;
    z-index: 999;
    color: white;
}

.card_title, .card_ogtitle, .card_vote{
    font-weight: bold;
}

.card_language{
    display: flex;
    align-items: center;
    gap: 5px;
}

.card_poster{
    width: 100%;
    height: 100%;
}

.star {
    color: rgb(230, 234, 49);
}
</style>