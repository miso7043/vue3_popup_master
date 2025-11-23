<template>
  <div v-if="isOpen" class="modal">
    <div class="modal-content">
      <h2>{{ title }}</h2>
      <p>{{ txtPromotion }}</p>
      <SlideBtn @click="handleClose" btnTitle="Close" btnType="btn-rect" fontSize="1.2rem" borderRadius="1rem"
        width="7rem" height="4rem" />
    </div>
  </div>
</template>

<script setup>
import SlideBtn from '../util/SlideButton.vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  title: {
    type: String,
    default: "Help"
  },
  txtPromotion: {
    type: String,
    default: "Here are some tips to get started..."
  }
})

const emit = defineEmits(['close'])

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
    display: grid;
    justify-items: center;

    h2 {
      margin-top: 0;
      font-size: 2rem;
      color: white;
    }

    p {
      margin: 0 0 20px;
      font-size: 1.3rem;
      color: white;
    }
  }
}
</style>
