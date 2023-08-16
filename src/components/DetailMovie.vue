<template>
  <button type="button" class="btn btn-primary" @click="openModal">Ver más</button>

  <div
    class="modal fade"
    id="modal_detail"
    tabindex="-1"
    aria-labelledby="modal_detail_label"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="exampleModalLabel">Detalles</h1>
          <button
            type="button"
            class="btn-close"
            v-on:click="closeModal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <div class="card mb-3 text-start">
            <div class="row g-0">
              <div class="col-4">
                <img v-bind:src="poster" class="img-thumbnail rounded-start" alt="title" />
              </div>
              <div class="col-8">
                <div class="card-body">
                  <h5 class="card-title">{{ title }}</h5>
                  <p class="card-text"><u>Year</u>: {{ year }}</p>
                  <p class="card-text"><u>Director</u>: {{ director }}</p>
                  <p class="card-text"><u>Director</u>: {{ actors }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" v-on:click="closeModal">Cerrar</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { Modal } from 'bootstrap'
import axios from 'axios'
export default {
  data() {
    return {
      title: '',
      year: '',
      director: '',
      actors: ''
    }
  },
  props: {
    imdbID: { String },
    poster: { String }
  },
  mounted() {
    this.loginModal = new Modal(document.getElementById('modal_detail'))
  },
  methods: {
    async openModal() {
      const url = `http://www.omdbapi.com/?apikey=d0e5d86d&i=${this.imdbID}`
      let response = await axios.get(url)
      const data = response.data

      this.title = data.Title
      this.year = data.Year
      this.director = data.Director
      this.actors = data.Actors

      this.loginModal.show()
    },
    closeModal() {
      this.loginModal.hide()
    }
  }
}
</script>
