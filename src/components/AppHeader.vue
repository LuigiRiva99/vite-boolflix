<template>
    <section class="header">
        <div class="container">
            <h1 class="title">
            Boolflix
            </h1>
            <div class="search_bar">
                <input type="search" placeholder="Cerca un prodotto" v-model="store.userInput" @keyup.enter="filmCall">
                <button @click="filmCall">search</button>
            </div>
        </div>
    </section>
</template>

<script>
import { store } from '../store.js'
import axios from 'axios'

export default {
    data() {
        return{
            store
        }
    },

    methods : {
    filmCall() {
        axios.get('https://api.themoviedb.org/3/search/movie',{
            params: {
                api_key: store.apiKey,
                query: store.userInput,
                }
        }
        ).then((res) => {
          store.filmList = res.data.results
          //console.log(store.filmList);
        }),
    
        axios.get('https://api.themoviedb.org/3/search/tv',{
            params: {
                api_key: store.apiKey,
                query: store.userInput
            }
        }).then((res) => {
            store.seriesList = res.data.results
            // console.log(store.seriesList);
        })

        store.userInput = ''
    }
  },
}
</script>

<style lang="scss" scoped>
.header{
    background-color: #1B1B1B;
    .container {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 10px;
        margin-bottom: 10px;
        .title{
            color: red;
        }

        button {
            margin-left: 10px;
            padding: 2px;
        }
    }
}

</style>