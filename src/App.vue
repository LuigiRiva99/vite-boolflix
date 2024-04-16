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

  data() {
    return {
      // apiKey: '8e629c4631d97d1396230a4e1f5b57c1',
      // query: 'ritorno al futuro'
    }
  },

  // methods : {
  //   filmCall() {
  //     axios.get('https://api.themoviedb.org/3/search/movie',{
  //       params: {
  //             api_key: this.apiKey,
  //             query: this.query,
  //           }
  //     }
  //     )
  //       .then((res) => {
  //         store.filmList = res.data.results
  //         console.log(store.filmList);
  //       })
  //   }
  // },

  // created() {
  //   this.filmCall()
  // }
};
</script>

<template>
  <AppHeader/>
  <AppMain/>
</template>

<style lang="scss">
@use './style/general'
</style>
