<script setup>
import { RouterLink, RouterView } from 'vue-router'
import axios from 'axios'
import LoginModal from './components/home/LoginModal.vue'
import UserModal from './components/home/UserModal.vue'

import { ref } from 'vue'
import { useRoute, useRouter } from 'vue-router'

const isAuthenticated = ref(false)
const route = useRoute()
const router = useRouter()

const checkAuthentication = () => {
  const token = localStorage.getItem('jwtToken')
  isAuthenticated.value = !!token
}

const logout = () => {
  localStorage.removeItem('jwtToken')
  router.push('/')
  window.location.reload()
}

checkAuthentication()
</script>

<template>
  <header>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
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
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <router-link to="/" class="nav-link"> Inicio </router-link>
            </li>
            <li class="nav-item" v-if="isAuthenticated">
              <router-link to="/favoritos" class="nav-link"> Favoritos </router-link>
            </li>
          </ul>
        </div>
        <div class="btn-group" role="group">
          <template v-if="!isAuthenticated">
            <LoginModal />
            <UserModal />
          </template>
          <template v-else>
            <button class="btn btn-dark" @click="logout">Cerrar Sesión</button>
          </template>
        </div>
      </div>
    </nav>
  </header>

  <RouterView />
</template>

<script>
export default {
  components: {
    LoginModal,
    UserModal
  }
}
</script>
