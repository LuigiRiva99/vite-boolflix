<template>
    <section class="header">
        <div class="container">
            <div class="logo">
                <img src="https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png" alt="">
            </div>
            <div class="search_bar">
                <input type="search" placeholder="Cerca un prodotto" v-model="store.userInput" @keyup.enter="filmCall" v-show="searchBarVisible">
                <!-- <button @click="filmCall">search</button> -->
                <font-awesome-icon class="search_icon" icon="search" @click="toggleSearch"/>
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
            store,
            searchBarVisible: false
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
        },

        toggleSearch() {
            this.searchBarVisible = !this.searchBarVisible
        }
  },
}
</script>

<style lang="scss" scoped>
.header{
    background-color: #1B1B1B;
    padding-bottom: 20px;
    .logo{
        max-width: 150px;
    }
    .container {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 10px;
        .title{
            color: red;
        }

        button {
            margin-left: 10px;
            padding: 2px;
        }

        .search_icon{
            color: white;

            &:hover {
                cursor: pointer;
            }
        }
    }
}

</style>