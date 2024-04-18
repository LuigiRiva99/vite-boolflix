<template>
    <div class="card" @mouseover="cardInfoToggle(true)" @mouseleave="cardInfoToggle(false)">
        <div class="card_info" v-show="cardInfo" >
            <p><span class="card_title">Titolo: </span>{{ title }}</p>
            <p><span class="card_ogtitle">Titolo og: </span> {{ originalTitle }}</p>
            <p class="card_language">
                <span class="card_vote">Lingua: </span>
                <img v-if="element.original_language === 'it'" width="30" height="30" src="https://img.icons8.com/emoji/48/italy-emoji.png" alt=""/>
                <img v-else-if="element.original_language === 'fr'" width="30" height="30" src="https://img.icons8.com/emoji/48/france-emoji.png" alt=""/>
                <img v-else-if="element.original_language === 'en'" width="30" height="30" src="https://img.icons8.com/emoji/48/us-outlying-islands-emoji.png" alt=""/>
                <img v-else-if="element.original_language === 'ja'" width="30" height="30" src="https://img.icons8.com/color/48/japan.png" alt="japan"/>
            </p>
            <p><span class="card_vote">Voto: </span><font-awesome-icon v-for="i in 5" :class="i <= starConverter(element.vote_average) ? 'star':''" icon="star"/></p>
            <p><span class="card_overview">Overview: </span>{{ element.overview }}</p>
        </div>
        <img class="card_poster" :src="isPosterAvailable()" alt="">
    </div>
</template>

<script>

export default {
    props : ['element','title','originalTitle'],

    data() {
        return{
            cardInfo: false,
        }
    },


    methods: {
        starConverter(vote) {
            const score =  Math.floor(vote / 2)
            return score
        },

        cardInfoToggle(status) {
            this.cardInfo = status
        },

        isPosterAvailable() {
            if (this.element.poster_path === null) {
                return `https://images.ctfassets.net/4cd45et68cgf/Rx83JoRDMkYNlMC9MKzcB/2b14d5a59fc3937afd3f03191e19502d/Netflix-Symbol.png?w=700&h=456`
            } else{
                return `https://image.tmdb.org/t/p/w342/${this.element.poster_path}`
            }
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

    p{
        margin: 10px 0px;  
        line-height: 22px; 
    }
    height: 100%;
    width: 100%;
    // display: flex;
    gap: 20px;
    padding: 20px;
    background-color: rgba( #1B1B1B,0.8);
    position: absolute;
    z-index: 999;
    color: white;
    white-space: normal; 
    overflow: auto;
}

.card_title, .card_ogtitle, .card_vote, .card_overview{
    font-weight: bold;
    color: rgb(255, 31, 31);
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