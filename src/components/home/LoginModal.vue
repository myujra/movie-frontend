<template>
  <!-- Button -->
  <button type="button" class="btn btn-success" @click="openModal">Iniciar Sesión</button>

  <!-- Modal -->
  <div
    class="modal fade"
    id="modal_login"
    tabindex="-1"
    aria-labelledby="modal_login_label"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="modal_login_label">Iniciar Sesión</h5>
          <button type="button" class="btn-close" aria-label="Close" @click="closeModal"></button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="login">
            <div class="mb-3">
              <label for="log_username" class="form-label">Usuario</label>
              <input
                type="text"
                class="form-control"
                id="log_username"
                required
                v-model="username"
              />
            </div>
            <div class="mb-3">
              <label for="log_password" class="form-label">Contraseña</label>
              <input
                type="password"
                class="form-control"
                id="log_password"
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
                <button type="submit" class="btn btn-success">Ingresar</button>
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

const url = 'http://localhost:3000/api/auth'
export default {
  data: () => ({ username: '', password: '' }),
  mounted() {
    this.loginModal = new Modal(document.getElementById('modal_login'))
  },
  methods: {
    async login() {
      const user = {
        username: this.username,
        password: this.password
      }
      const response = await axios.post(url + '/login', user)
      const token = response.data.token
      localStorage.setItem('jwtToken', token)

      this.closeModal()

      window.location.reload()
    },
    cleanForm() {
      this.username = ''
      this.password = ''
    },
    openModal() {
      this.loginModal.show()
    },
    closeModal() {
      this.loginModal.hide()
      this.cleanForm()
    }
  }
}
</script>
