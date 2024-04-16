<template>
    <section class="main_page">
        <div class="container">
            <h2 v-if="store.filmList.length !== 0">Films</h2>
            <ul class="row">
                <h2 v-if="store.filmList.length === 0"  class="no_results">Nessun film trovato</h2>
                <li v-for="film in store.filmList">
                    <AppCard :element="film" :title="film.title" :originalTitle="film.original_title"/>
                </li>
            </ul>
            <h2 v-if="store.seriesList.length !== 0">Series</h2>
            <ul class="row">
                <h2 v-if="store.seriesList.length === 0" class="no_results">Nessuna serie TV trovata</h2>
                <li v-for="series in store.seriesList">
                    <AppCard :element="series" :title="series.name" :originalTitle="series.original_name"/>
                </li>
            </ul>
        </div>
    </section>
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

.main_page{
    background-color: #1B1B1B;
    color: white;
    height: 100%;
}

.container{
    margin: 0 20px;
    max-width: 1200px;
}

.flex {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: flex-start;
}

.row{
    display: flex;
}

.no_results {
    margin: 15px;
    opacity: 0.2;
}


</style>