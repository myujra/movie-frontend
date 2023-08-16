<template>
  <div class="card text-center">
    <img class="card-img-top img-thumbnail" v-bind:src="poster" alt="Card image cap" />
    <div class="card-body">
      <div class="mb-2">
        <DetailMovie :poster="poster" :imdbID="imdbID" />
      </div>
      <button
        type="button"
        class="btn btn-outline-danger"
        v-on:click="addToFavorites"
        v-if="!favorite"
      >
        Añadir a mis películas
      </button>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
import DetailMovie from './DetailMovie.vue'
const url = 'http://localhost:3000/api/movies'
export default {
  props: {
    imdbID: { String },
    poster: { String },
    favorite: { Boolean }
  },
  components: {
    DetailMovie
  },
  methods: {
    async addToFavorites() {
      try {
        const token = localStorage.getItem('jwtToken')

        let responseMovie = await axios.get(
          `http://www.omdbapi.com/?apikey=d0e5d86d&i=${this.imdbID}`
        )
        const data = responseMovie.data

        const response = await axios.post(
          url + '/favorites',
          {
            poster: data.Poster,
            title: data.Title,
            year: data.Year,
            director: data.Director,
            actors: data.Actors
          },
          { headers: { Authorization: token } }
        )
      } catch (error) {
        console.error('Error adding to favorites:', error.response.data.message)
      }
    }
  }
}
</script>
