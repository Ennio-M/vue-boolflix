<template>
  <div id="app">
    <header>
      <h1>BOOLFLIX</h1>
      <search-bar @search="getAll"/>
    </header>
    <main>
      <app-grid :items="moviesArray" what="Film"/>
      <app-grid :items="seriersArray" what="Serie"/>
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
      moviesArray: [],
      seriersArray: [],
    }
  },
  methods: {
    getMovies(queryParams) {
      return axios.get(`${this.apiPath}movie`, queryParams).catch((error) => {console.log(error)})
    },
    getSeries(queryParams) {
      return axios.get(`${this.apiPath}tv`, queryParams).catch((error) => {console.log(error)})
    },
    getAll(txt) {
      const queryParams = {
        params: {
          api_key: this.apiKey,
          query: txt
        }
      }
      Promise.all([this.getMovies(queryParams), this.getSeries(queryParams)])
      .then((results) => {
        this.moviesArray = results[0].data.results;
        this.seriersArray = results[1].data.results;
      })
    }
  }
}
</script>

<style lang="scss">
  @import './styles/general.scss';
</style>
