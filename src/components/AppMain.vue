<template>
    <ul>
        <li v-for="film in store.filmList">
            <p>Titolo: {{ film.title }}</p>
            <p>Titolo og: {{ film.original_title }}</p>
            <p>Lingua: {{ film.original_language }}</p>
            <p>Voto: {{ film.vote_average }}</p>
        </li>
    </ul>
</template>

<script>
import { store } from '../store.js'

export default {
    data(){
        return {
            store
        }
    }
}
</script>

<style lang="scss" scoped>

</style>