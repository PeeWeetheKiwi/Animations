<template>
  <div v-if="open" class="backdrop" @click="$emit('close')"></div>
  <transition name="modal">
    <dialog open v-if="open">
      <slot></slot>
    </dialog>
  </transition>
</template>

<script>
export default {
  props: ['open'],
  emits: ['close']
};
</script>

<style scoped>
.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  z-index: 10;
  background-color: rgba(0, 0, 0, 0.75);
  opacity: 45%;
}

dialog {
  position: fixed;
  top: 30vh;
  width: 30rem;
  left: calc(50% - 15rem);
  margin: 0;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  border-radius: 12px;
  padding: 1rem;
  background-color: white;
  z-index: 100;
  border: none;
}

.modal-enter-active {
  animation: modal-boy 0.7s ease-in-out forwards;
}

.modal-leave-active {
  animation: modal-boy 0.7s ease-in-out reverse;
}

@keyframes modal-boy {
  from{
    opacity: 0;
    transform: scale(0.5) rotate(0);
  }
  to{
    opacity: 1;
    transform: scale(1) rotate(360deg);
  }
}


</style>