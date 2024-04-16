<script>
import axios from 'axios'
import { store } from './store.js'
import AppHeader from './components/AppHeader.vue'
import AppMain from './components/AppMain.vue'

export default {
  components: {
    AppHeader,
    AppMain
  },

  methods : {
    filmCall() {
      axios.get('https://api.themoviedb.org/3/search/movie?api_key=8e629c4631d97d1396230a4e1f5b57c1&query=ritorno al futuro')
        .then((res) => {
          store.filmList = res.data.results
          console.log(store.filmList);
        })
    }
  },

  created() {
    this.filmCall()
  }
};
</script>

<template>
  <AppHeader/>
  <AppMain/>
</template>

<style>

</style>
