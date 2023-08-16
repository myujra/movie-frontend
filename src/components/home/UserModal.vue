<template>
  <button type="button" class="btn btn-primary" @click="openModal">
    <i class="fa fa-user-plus" aria-hidden="true"></i>
  </button>

  <div
    class="modal fade"
    id="modal_register"
    tabindex="-1"
    aria-labelledby="modal_register_label"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="modal_register_label">Modal title</h5>
          <button type="button" class="btn-close" aria-label="Close" @click="closeModal"></button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="register">
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
              <input type="text" class="form-control" id="last_name" required v-model="last_name" />
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
            <hr />
            <div class="row">
              <div class="col">
                <button type="button" class="btn btn-outline-secondary" @click="closeModal">
                  Cerrar
                </button>
              </div>
              <div class="col text-end">
                <button type="submit" class="btn btn-primary">Registrar</button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { Modal } from 'bootstrap'
import axios from 'axios'

const url = 'http://localhost:3000/api/users'

export default {
  data: () => ({ first_name: '', last_name: '', username: '', password: '' }),
  mounted() {
    this.loginModal = new Modal(document.getElementById('modal_register'))
  },
  methods: {
    async register() {
      const user = {
        first_name: this.first_name,
        last_name: this.last_name,
        username: this.username,
        password: this.password
      }
      await axios.post(url + '/register', user)

      this.closeModal()
    },
    openModal() {
      this.loginModal.show()
    },
    closeModal() {
      this.loginModal.hide()
    }
  }
}
</script>
