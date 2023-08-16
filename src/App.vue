<script setup>
import { RouterLink, RouterView } from 'vue-router'
import axios from 'axios'
import LoginModal from './components/home/LoginModal.vue'
import UserModal from './components/home/UserModal.vue'
</script>

<template>
  <header>
    <nav class="navbar navbar-dark bg-dark">
      <div class="container-fluid">
        <router-link to="/" class="navbar-brand">
          <img
            src="@/assets/logo.svg"
            alt="Logo"
            width="30"
            height="24"
            class="d-inline-block align-text-top"
          />
          Examen Desarrollador
        </router-link>

        <div class="btn-group" role="group">
          <!-- <button
            class="btn btn-success"
            type="button"
            data-bs-toggle="modal"
            data-bs-target="#loginModal"
            v-on:click="cleanForm"
          >
            Iniciar Sesión
          </button> -->

          <LoginModal />
          <UserModal />
        </div>
      </div>
    </nav>

    <!-- Modal Registro -->
    <div
      class="modal fade"
      id="register"
      tabindex="-1"
      data-bs-backdrop="static"
      data-bs-keyboard="false"
      aria-labelledby="registerLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="registerLabel">Registro de Usuario</h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <form @submit.prevent="registerUser">
              <div class="mb-3">
                <label for="first_name" class="form-label">Nombre</label>
                <input
                  type="text"
                  class="form-control"
                  id="first_name"
                  required
                  v-model="first_name"
                />
              </div>
              <div class="mb-3">
                <label for="last_name" class="form-label">Apellido</label>
                <input
                  type="text"
                  class="form-control"
                  id="last_name"
                  required
                  v-model="last_name"
                />
              </div>
              <div class="mb-3">
                <label for="username" class="form-label">Usuario</label>
                <input type="text" class="form-control" id="username" required v-model="username" />
              </div>
              <div class="mb-3">
                <label for="password" class="form-label">Contraseña</label>
                <input
                  type="password"
                  class="form-control"
                  id="password"
                  required
                  v-model="password"
                />
              </div>

              <div class="modal-footer">
                <button
                  type="button"
                  class="btn btn-outline-secondary"
                  data-bs-dismiss="modal"
                  v-on:click="cleanForm"
                >
                  Cerrar
                </button>
                <button type="submit" class="btn btn-primary">Guardar</button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </header>

  <RouterView />
</template>

<script>
export default {
  components: {
    LoginModal,
    UserModal
  },
  data: () => ({
    first_name: '',
    last_name: '',
    username: '',
    password: ''
  }),
  methods: {
    async registerUser() {
      const url = 'http://localhost:3000/api/users/register'
      const user = {
        first_name: this.first_name,
        last_name: this.last_name,
        username: this.username,
        password: this.password
      }
      console.log(user)
      await axios.post(url, user)
      new bootstrap.Modal(document.getElementById('add_userModal'), {}).hide()
      this.cleanForm()
    },
    cleanForm() {
      this.first_name = ''
      this.last_name = ''
      this.username = ''
      this.password = ''
    }
  }
}
</script>
