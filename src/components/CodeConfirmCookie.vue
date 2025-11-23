<template>
  <div class="codeBox">
    <CodeViewer :code="codeData" :title="codeFileName" height="400px" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import CodeViewer from '../util/CodeViewer.vue';

const codeFileName = "Modal.vue";
const codeData = `<template>
  <div v-if="isOpen" class="cookie">
    <div v-if="!hasAccepted" class="cookie-content">
      <p class="cookie-text">{{ cookieText }}</p>
      <SlideBtn @click="acceptCookies" btnTitle="동의" btnType="btn-rect" fontSize="1.2rem" borderRadius="1rem"
        width="7rem" height="4rem" />
    </div>
  </div>
</template>

<\script setup>
import { ref } from 'vue'
import SlideBtn from '../util/SlideButton.vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  cookieText: {
    type: String,
    default: '이 웹사이트는 쿠키를 사용합니다.'
  },
})

const hasAccepted = ref(false)

const acceptCookies = () => {
  hasAccepted.value = true
  
  handleClose();
}

const emit = defineEmits(['close'])

const handleClose = () => {
  emit('close')
}
</\script>

<style lang="scss" scoped>
.cookie {
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

  .cookie-content {
    margin: auto;
    padding: 30px;
    border-radius: 1rem;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
    max-width: 80%;
    width: 400px;
    text-align: center;
    background-color: #2c2c2c;
    border: 2px solid #023c24;
    display: grid;
    justify-items: center;

    .cookie-text {
      font-size: 1.3rem;
      margin-bottom: 30px;
      color: white;
      font-weight: 500;
    }
  }
}
</style>`;
</script>

<style lang="scss" scoped>
</style>