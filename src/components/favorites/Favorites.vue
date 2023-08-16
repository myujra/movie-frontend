<template>
  <div class="container mt-3">
    <h1>Favoritos</h1>
    <hr />
    <div class="row">
      <div class="col-lg-3 col-md-4 mb-2 col-sm-6" v-for="(movie, index) in favorites" :key="index">
        <CardMovie :poster="movie.poster" :imdbID="movie.imdbID" :favorite="true" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import CardMovie from '../CardMovie.vue'
import DetailMovie from '../DetailMovie.vue'

const url = 'http://localhost:3000/api/movies'
export default {
  data() {
    return {
      favorites: []
    }
  },
  components: {
    CardMovie,
    DetailMovie
  },
  methods: {
    async getMovies() {
      const token = localStorage.getItem('jwtToken')
      let response = await axios.get(url + '/favorites', { headers: { Authorization: token } })
      this.favorites = response.data
    }
  },
  async created() {
    await this.getMovies()
  }
}
</script>
