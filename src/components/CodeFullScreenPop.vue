<template>
  <div class="codeBox">
    <CodeViewer :code="codeData" :title="codeFileName" height="400px" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import CodeViewer from '../util/CodeViewer.vue';

const codeFileName = "FullScreenPop.vue";
const codeData = `<template>
  <div v-if="isOpen" class="fullscreen-modal">
    <div class="modal-content">
      <h2>Fullscreen Popup</h2>
      <SlideBtn @click="handleClose" btnTitle="Close" btnType="btn-rect" fontSize="1.2rem" borderRadius="1rem"
        width="7rem" height="4rem" />
    </div>
  </div>
</template>

<\script setup>
import { defineEmits } from 'vue';
import SlideBtn from '../util/SlideButton.vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits(['close'])

const handleClose = () => {
  emit('close')
}
</\script>

<style lang="scss" scoped>
.fullscreen-modal {
  position: fixed;
  z-index: 1000;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8); // 투명도 80%
  display: flex;
  align-items: center;
  justify-content: center;

  .modal-content {
    background-color: #2c2c2c;
    padding: 30px;
    border-radius: 1rem;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
    border: 2px solid #023c24;
    color: white;
    width: calc(100% - 30px);
    height: calc(100% - 30px);
    text-align: center;
    position: relative;
    display: grid;
    justify-items: center;
    align-content: space-evenly;
    
    h2 {
      margin-bottom: 20px;
      font-size: 2rem;
    }

    .btn {
      padding: 12px 25px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1rem;
      font-weight: 600;
      transition: all 0.3s ease;

      &.btn-confirm {
        background-color: #4A90E2;
        color: white;

        &:hover {
          background-color: #357ABD;
          transform: translateY(-2px);
        }
      }

      &.btn-cancel {
        background-color: #E2E2E2;
        color: #333;

        &:hover {
          background-color: #D1D1D1;
          transform: translateY(-2px);
        }
      }
    }
  }
}
</style>`;
</script>

<style lang="scss" scoped>
</style>