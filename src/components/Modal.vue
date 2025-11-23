<template>
  <div v-if="isOpen" class="modal">
    <div class="modal-content" :style="contentStyle">
      <span @click="handleClose" class="close">&times;</span>
      <h2 v-if="title" class="modal-title">{{ title }}</h2>
      <p class="modal-text">{{ txtContent }}</p>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  width: {
    type: String,
    default: '500px'
  },
  height: {
    type: String,
    default: 'auto'
  },
  title: {
    type: String,
    default: ''
  },
  txtContent: {
    type: String,
    default: 'Basic Modal Popup'
  }
})

const emit = defineEmits(['close'])

const handleClose = () => {
  emit('close')
}

const contentStyle = computed(() => ({
  width: props.width,
  height: props.height
}))
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
    background-color: #2c2c2c;
    margin: auto;
    padding: 30px;
    border-radius: 1rem;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
    max-width: 80%;
    width: 400px;
    text-align: center;
    border: 2px solid #023c24;
    color: white;
    position: relative;

    .close {
      position: absolute;
      top: 10px;
      right: 10px;
      color: #aaaaaa;
      font-size: 28px;
      font-weight: bold;
      cursor: pointer;
      line-height: 1;

      &:hover,
      &:focus {
        color: #000;
        text-decoration: none;
      }
    }

    .modal-title {
      margin-top: 20px;
      margin-bottom: 15px;
      font-size: 2rem;
      color: white;
    }

    .modal-text {
      font-size: 1.5rem;
      line-height: 1.5;
      margin: 1rem auto;
      color: white;
    }
  }
}
</style>
