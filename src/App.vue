<script setup>
import { RouterLink, RouterView } from 'vue-router'
import axios from 'axios'
import LoginModal from './components/home/LoginModal.vue'
import UserModal from './components/home/UserModal.vue'
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
            <li class="nav-item">
              <router-link to="/favoritos" class="nav-link"> Favoritos </router-link>
            </li>
          </ul>
        </div>
        <div class="btn-group" role="group">
          <LoginModal />
          <UserModal />
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
