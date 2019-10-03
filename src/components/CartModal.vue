<template>
  <div v-if="cartToggle">
    <div class="modal" tabindex="-1">
      <div class="modal-dialog">
        <div class="modal-header">
          <h2>Shopping Cart</h2>
          <button
            class="close font-weight-bold"
            v-on:click="this.handleClose"
            aria-label="close"
          >
            <span>X</span>
          </button>
        </div>

      </div>
    </div>
    <div class="modal-backdrop"></div>
  </div>
</template>

<script>
export default {
  name: "CartModal"
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.modal {
  position: fixed;
  z-index: 1050;
  display: block;
  width: 100%;
  outline: 0;
}
.modal-dialog {
  position: relative;
  flex: 0 0 auto;
  width: auto;
  height: auto;
  margin: 0.5 auto;
  padding: 2.5rem 1.5rem;
  background-color: white;
  // z-index: 1051;
  // overflow-y: auto;
  pointer-events: auto;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1040;
  background-color: #22211f;
  opacity: 0.8;
}
.modal-header {
  border-bottom: none;
  padding: 0;
}
.close {
  padding: 0rem 1rem;
  pointer-events: auto;
}

body {
  overflow: hidden;
}
</style>
