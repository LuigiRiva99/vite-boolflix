<template>
    <section class="main_page">
        <div class="flex container">
            <ul>
                <h2 v-if="store.filmList.length === 0"  class="no_results">Nessun film trovato</h2>
                <h2 v-if="store.filmList.length !== 0">Films</h2>
                <li v-for="film in store.filmList">
                    <AppCard :element="film" :title="film.title" :originalTitle="film.original_title"/>
                </li>
            </ul>
            <ul>
                <h2 v-if="store.seriesList.length === 0" class="no_results">Nessuna serie TV trovata</h2>
                <h2 v-if="store.seriesList.length !== 0">Series</h2>
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
.container{
    margin: 0 auto;
    max-width: 1200px;
}

.flex {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: flex-start;
}

.no_results {
    margin: 15px;
    opacity: 0.2;
}


</style>