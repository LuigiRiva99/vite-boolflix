<template>
    <div>
        <p>Titolo: {{ title }}</p>
        <p>Titolo og: {{ originalTitle }}</p>
        <p>Lingua: {{ element.original_language }} 
            <img v-if="element.original_language === 'it'" width="30" height="30" src="https://img.icons8.com/emoji/48/italy-emoji.png" alt=""/>
            <img v-if="element.original_language === 'fr'" width="30" height="30" src="https://img.icons8.com/emoji/48/france-emoji.png" alt=""/>
            <img v-if="element.original_language === 'en'" width="30" height="30" src="https://img.icons8.com/emoji/48/us-outlying-islands-emoji.png" alt=""/>
            <img v-if="element.original_language === 'ja'" width="30" height="30" src="https://img.icons8.com/color/48/japan.png" alt="japan"/>
        </p>
        <p>Voto: {{ starConverter(element.vote_average) }} <font-awesome-icon v-for="i in 5" :class="i <= starConverter(element.vote_average) ? 'star':''" icon="star"/></p>
        <img :src="`https://image.tmdb.org/t/p/w154/${element.poster_path}`" alt="">
    </div>
</template>

<script>

import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { library } from '@fortawesome/fontawesome-svg-core'
import { faStar } from '@fortawesome/free-solid-svg-icons'
// import { faSearch } from '@fortawesome/free-solid-svg-icons'

library.add(faStar)
// library.add(faSearch)

export default {
    props : ['element','title','originalTitle'],

    components:{
        FontAwesomeIcon
    },

    methods: {
        starConverter(vote) {
            const score =  Math.floor(vote / 2)
            return score
        }
    }
}
</script>

<style lang="scss" scoped>

.star {
    color: rgb(230, 234, 49);
}
</style>