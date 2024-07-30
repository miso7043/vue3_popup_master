<template>
  <div v-if="isOpen" class="modal">
    <div class="modal-content">
      <p class="modal-text">{{ text }}</p>
      <div class="button-container">
        <SlideBtn class="btn-confirm" @click="confirm" :btnTitle="confirmText" btnType="btn-rect" fontSize="1.2rem"
          borderRadius="1rem" width="7rem" height="4rem" />
        <SlideBtn class="btn-cancel" @click="handleClose" :btnTitle="cancelText" btnType="btn-rect" fontSize="1.2rem"
          borderRadius="1rem" width="7rem" height="4rem" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'
import SlideBtn from '../util/SlideButton.vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  text: {
    type: String,
    default: 'Are you sure?'
  },
  confirmText: {
    type: String,
    default: 'Yes'
  },
  cancelText: {
    type: String,
    default: 'No'
  }
})

const emit = defineEmits(['close', 'confirm'])

const confirm = () => {
  emit('confirm')
  handleClose()
}

const handleClose = () => {
  emit('close')
}
</script>

<style lang="scss" scoped>
.modal {
  position: fixed;
  z-index: 1000;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;

  .modal-content {
    margin: auto;
    padding: 30px;
    border-radius: 1rem;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
    max-width: 80%;
    width: 400px;
    text-align: center;
    background-color: #2c2c2c;
    border: 2px solid #023c24;

    .modal-text {
      font-size: 1.3rem;
      margin-bottom: 30px;
      color: white;
      font-weight: 500;
    }

    .button-container {
      display: flex;
      justify-content: center;
      gap: 20px;
    }
    // }
  }
}
</style>