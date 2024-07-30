<template>
  <div v-if="isOpen" class="notification">
    <p>{{ message }}</p>
    <SlideBtn @click="handleClose" btnTitle="Close" btnType="btn-rect" fontSize="1.2rem"
          borderRadius="1rem" width="7rem" height="4rem" />
  </div>
</template>

<script setup>
import { defineProps } from 'vue';
import SlideBtn from '../util/SlideButton.vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  message: {
    type: String,
    default: 'This is a notification!'
  }
})

const emit = defineEmits(['close'])

const handleClose = () => {
  emit('close')
}
</script>

<style lang="scss" scoped>
.notification {
  position: fixed;
  z-index: 10;
  left: 50%;
  top: 40%;
  transform: translateX(-50%);
  background-color: #2c2c2c;
  padding: 20px 30px;
  border-radius: 1rem;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  border: 2px solid #023c24;
  color: white;
  text-align: center;
  max-width: 80%;
  width: 400px;
  display:grid;
  justify-items: center;

  p {
    margin: 0 0 20px;
    font-size: 1.3rem;
  }
}
</style>
