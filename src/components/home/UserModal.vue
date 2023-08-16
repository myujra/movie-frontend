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
        <div class="modal-body">...</div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" @click="closeModal">Close</button>
          <button type="button" class="btn btn-primary">Save changes</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { Modal } from 'bootstrap'
export default {
  data: () => ({ theModal: null, username: '', password: '' }),
  mounted() {
    this.loginModal = new Modal(document.getElementById('modal_register'))
  },
  methods: {
    openModal() {
      this.loginModal.show()
    },
    closeModal() {
      this.loginModal.hide()
    }
  }
}
</script>
