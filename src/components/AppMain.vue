<template>
    <div class="flex">
        <ul>
            <h2>Films</h2>
            <li v-for="film in store.filmList">
                <AppCard :element="film" :title="film.title" :originalTitle="film.original_title"/>
            </li>
        </ul>
        <ul>
            <h2>Series</h2>
            <li v-for="series in store.seriesList">
                <AppCard :element="series" :title="series.name" :originalTitle="series.original_name"/>
            </li>
        </ul>
    </div>
</template>

<script>
import { store } from '../store.js'
import AppCard from './AppCard.vue'

export default {
    components: {
        AppCard
    },
    data(){
        return {
            store
        }
    }
}
</script>

<style lang="scss" scoped>
.flex {
    display: flex;
}
</style>