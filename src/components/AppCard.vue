<template>
        <p>Titolo: {{ title }}</p>
        <p>Titolo og: {{ originalTitle }}</p>
        <p>Lingua: {{ element.original_language }} 
            <img v-if="element.original_language === 'it'" width="30" height="30" src="https://img.icons8.com/emoji/48/italy-emoji.png" alt=""/>
            <img v-if="element.original_language === 'fr'" width="30" height="30" src="https://img.icons8.com/emoji/48/france-emoji.png" alt=""/>
            <img v-if="element.original_language === 'en'" width="30" height="30" src="https://img.icons8.com/emoji/48/us-outlying-islands-emoji.png" alt=""/>
            <img v-if="element.original_language === 'ja'" width="30" height="30" src="https://img.icons8.com/color/48/japan.png" alt="japan"/>
        </p>
        <p>Voto: {{ starConverter(element.vote_average) }}</p>
        <img :src="`https://image.tmdb.org/t/p/w154/${element.poster_path}`" alt="">
</template>

<script>

export default {
    props : ['element','title','originalTitle'],

    methods: {
        starConverter() {
            const score =  Math.floor(vote / 2)
            return score
        }
    }
}
</script>

<style lang="scss" scoped>

</style>