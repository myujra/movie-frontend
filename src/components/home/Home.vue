<template>
  <div class="container mt-3">
    <div class="input-group mb-3">
      <input type="text" class="form-control" placeholder="Buscar por titulo" v-model="text" />
      <div class="input-group-append">
        <button class="btn btn-outline-primary" type="button" v-on:click="getMovies">
          <i class="fa fa-search"></i>
        </button>
      </div>
    </div>

    <div class="row">
      <div class="col-lg-3 col-md-4 mb-2 col-sm-6" v-for="(movie, index) in movies" :key="index">
        <CardMovie :poster="movie.Poster" :imdbID="movie.imdbID"> </CardMovie>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import CardMovie from '../CardMovie.vue'
import DetailMovie from '../DetailMovie.vue'
export default {
  data() {
    return {
      text: '',
      movies: []
    }
  },
  components: {
    CardMovie,
    DetailMovie
  },
  methods: {
    async getMovies() {
      const url = `http://www.omdbapi.com/?apikey=d0e5d86d&s=${this.text}`
      let response = await axios.get(url)
      this.movies = response.data.Search
    }
  }
}
</script>
