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
