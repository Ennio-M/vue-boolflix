<template>
  <div id="app">
    <header>
      <h1>BOOLFLIX</h1>
      <search-bar @search="searchArray"/>
    </header>
    <main>
      <app-grid :movies="moviesArray"/>
    </main>
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue';
import AppGrid from './components/AppGrid.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    SearchBar,
    AppGrid
  },
  data() {
    return {
      apiPath: 'https://api.themoviedb.org/3/search/',
      apiKey: 'b01146b2d3706fbbee082c9767602fd1',
      moviesArray: []
    }
  },
  methods: {
    getMovies(queryParams) {
      axios.get(`${this.apiPath}movie`, queryParams).then((res) => {
        this.moviesArray = res.data.results;
      }).catch((error) => {console.log(error)})
    },
    searchArray(txt) {
      const queryParams = {
        params: {
          api_key: this.apiKey,
          query: txt
        }
      }
      this.getMovies(queryParams)
    }
  }
}
</script>

<style lang="scss">
  @import './styles/general.scss';
</style>
