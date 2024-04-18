<template>
    <section class="main_page">
        <div class="container">
            <h2 v-if="store.filmList.length !== 0">Films</h2>
            <ul class="row">
                <h2 v-if="store.filmList.length === 0"  class="no_results">Nessun film trovato</h2>
                <div class="slide_container row" ref="container_film">
                    <li v-for="film in store.filmList">
                        <AppCard :element="film" :title="film.title" :originalTitle="film.original_title" ref="card"/>
                    </li>
                </div>
                <button v-if="store.filmList.length !== 0" class="button_right" @click="scrollRightFilm"><font-awesome-icon icon="arrow-right" class="arrow"/></button>
                <button v-if="store.filmList.length !== 0" class="button_left" @click="scrollLeftFilm"><font-awesome-icon icon="arrow-left" class="arrow"/></button>
            </ul>
            <h2 v-if="store.seriesList.length !== 0">Series</h2>
            <ul class="row">
                <h2 v-if="store.seriesList.length === 0" class="no_results">Nessuna serie TV trovata</h2>
                <div class="slide_container row" ref="container_series">
                    <li v-for="series in store.seriesList">
                        <AppCard :element="series" :title="series.name" :originalTitle="series.original_name"/>
                    </li>
                </div>
                <button v-if="store.filmList.length !== 0" class="button_right" @click="scrollRightSeries"><font-awesome-icon icon="arrow-right" class="arrow"/></button>
                <button v-if="store.filmList.length !== 0" class="button_left" @click="scrollLeftSeries"><font-awesome-icon icon="arrow-left" class="arrow"/></button>
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
    },

    methods: {
        //Film
        scrollRightFilm() {
            //this.$refs lo uso per selezionare il container con il ref container_film
            this.$refs.container_film.scrollBy({
                left: 300, 
                behavior: "smooth"
            });
        },
        scrollLeftFilm() {
            this.$refs.container_film.scrollBy({
                left: -300, 
                behavior: "smooth"
            });
        },

        //serieTV
        scrollRightSeries() {
            //this.$refs lo uso per selezionare il container con il ref container_series
            this.$refs.container_series.scrollBy({
                left: 300, 
                behavior: "smooth"
            });
        },
        scrollLeftSeries() {
            this.$refs.container_series.scrollBy({
                left: -300, 
                behavior: "smooth"
            });
        },
    }
}
</script>

<style lang="scss" scoped>
@use '../style/partials/variables' as *;

.main_page{
    background-color: $brand-color;
    color: white;
    height: 100%;
}

.container{
    margin: 0 20px;
    height: 100%;
    .row{
        display: flex;
        position: relative;
        .slide_container {
            width: 100%;
            overflow-x: hidden;
            white-space: nowrap;
        }
        .button_right, .button_left{
            width: 40px;
            height: 40px;
            position: absolute;
            border-radius: 999px;
            background-color:$brand-color;
            opacity: 0.5;
            color: white;
            border: none;
            &:hover{

                .arrow {
                    transition: transform 0.3s ease;
                    transform: scale(1.5);

                    &:active {
                        transition: transform 0.1s ease;
                        transform: scale(0.8);
                    }
                }
                cursor: pointer;
                color: red;
                opacity: 1;
            }
        }

        .button_right {
            top: 50%;
            left: 96%;
            margin-top: -25px;
            z-index: 999;
        }
        .button_left {
            top: 50%;
            left: 10px;
            margin-top: -25px;
            z-index: 999;
        }
    }
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