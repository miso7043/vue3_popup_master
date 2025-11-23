<template>
  <div class="codeBox">
    <CodeViewer :code="codeData" :title="codeFileName" height="400px" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import CodeViewer from '../util/CodeViewer.vue';

const codeFileName = "ImagePop.vue";
const codeData = `<template>
  <div>
    <div v-if="isOpen" class="lightbox" @click="handleClose">
      <img :src="imgPath" alt="fullsize Image" :style="{ width: imgWidth, height: imgHeight }" />
    </div>
  </div>
</template>

<\script setup>

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  imgPath: {
    type: String,
    default: "../src/assets/dlalwl/imgSample_1.avif"
  },
  imgWidth: {
    type: String,
    default: 'auto'
  },
  imgHeight: {
    type: String,
    default: 'auto'
  }
})

const emit = defineEmits(['close'])

const handleClose = () => {
  emit('close')
}
</\script>

<style lang="scss" scoped>
.lightbox {
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

  img {
    max-width: 80%;
    max-height: 80%;
    border: 2px solid #023c24;
    border-radius: 1rem;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  }
}
</style>
`;
</script>

<style lang="scss" scoped>
</style>