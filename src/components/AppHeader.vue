<template>
    <section class="header">
        <div class="container">
            <div class="home">
                <div class="logo">
                    <img src="https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png" alt="">
                </div>
                <div class="nav">
                    <ul class="nav_list">
                        <li><a href="#">Home</a></li>
                        <li><a href="#">Serie TV</a></li>
                        <li><a href="#">Film</a></li>
                        <li><a href="#">Originali</a></li>
                    </ul>
                </div>
            </div>
            <div class="search_section">
                <select v-show="searchBarVisible" name="language_select" class="language_select" v-model="store.language">
                    <option value="it-IT" selected>IT</option>
                    <option value="us-US">US</option>
                </select>
                <input class="search_bar" type="search" placeholder="Cerca un prodotto" v-model="store.userInput" @keyup.enter="filmCall" v-show="searchBarVisible">
                <button class="search_button" @click="filmCall" v-show="searchBarVisible">Cerca</button>
                <font-awesome-icon class="search_icon" icon="search" @click="toggleSearch" v-show="!searchBarVisible"/>
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
            searchBarVisible: false,
        }
    },

    methods : {
        filmCall() {
            axios.get('https://api.themoviedb.org/3/search/movie',{
                params: {
                    api_key: store.apiKey,
                    query: store.userInput,
                    language: store.language
                }
            }).then((res) => {
            store.filmList = res.data.results
            //console.log(store.filmList);
            }),
        
            axios.get('https://api.themoviedb.org/3/search/tv',{
                params: {
                    api_key: store.apiKey,
                    query: store.userInput,
                    language: store.language
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
@use '../style/partials/variables' as *;
.header{
    background-color: $brand-color;
    padding-bottom: 20px;
    .logo{
        max-width: 150px;
    }
    .container {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 10px;

        .home{
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;

            .nav_list{
                display: flex;
                gap: 20px;
                margin-left: 50px;

                li:hover {
                    font-weight: bold;
                }
            }
        }
        .title{
            color: red;
        }

        button {
            padding: 2px;
        }

        .search_section{
            display: flex;
            align-items: center;

            .language_select{
                margin-right: 10px;
                max-width: 50px;
                height: 30px;
                color: $brand-color;
                background-color: white;
                border: 1px solid transparent;
                border-radius: 10px;
            }
            .search_bar{
                margin-right: 10px;
                outline:none;
                padding: 5px;
                border-radius: 10px;
                border: 1px solid transparent;
                transition: border-color 0.3s ease;
                &:focus {
                    border-color: red;
                    box-shadow: 0 0 10px red;
                }
            }

            .search_button {
                height: 30px;
                border-radius: 10px;
                background-color: white;
                border-color: red;
                border: 1px solid transparent;
                line-height: 10px;
                padding: 10px;
                &:hover{
                    cursor: pointer;
                    background-color: $brand-color;
                    color: red;
                    border-color: red;
                }
            }
    
            .search_icon{
                color: white;
    
                &:hover {
                    cursor: pointer;
                }
            }
        }
    }
}

</style>