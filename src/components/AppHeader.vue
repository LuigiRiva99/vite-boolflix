<template>
    <h1>
    Boolflix
    </h1>
    <input type="search" v-model="store.userInput">
    <button @click="filmCall">search</button>
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
      )
        .then((res) => {
          store.filmList = res.data.results
          console.log(store.filmList);
        })
    }
  },
}
</script>

<style lang="scss" scoped>

</style>