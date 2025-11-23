<template>
  <div v-if="isVisible" class="notification" :style="notificationStyle">
    <p>{{ txtMessage }}</p>
    <button @click="hideToast" class="close">X</button>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  txtMessage: {
    type: String,
    default: "A new message has arrived!"
  },
  popWidth: {
    type: String,
    default: "500px"
  },
  popHeight: {
    type: String,
    default: "auto"
  }
})

const isVisible = ref(false)

const emit = defineEmits(['close'])

const hideToast = () => { 
  isVisible.value = false;
  emit('close');
}

onMounted(() => {
  isVisible.value = props.isOpen;
  
  if (isVisible.value) {
    setTimeout(() => {
      hideToast();
    }, 3000);
  }
});

const notificationStyle = computed(() => ({
  width: props.popWidth,
  height: props.popHeight
}));
</script>

<style lang="scss" scoped>
.notification {
  position: fixed;
  z-index: 1000;
  left: 50%;
  bottom: 20px;
  transform: translateX(-50%);
  background-color: #f3faae;
  padding: 20px 30px;
  border-radius: 1rem;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  border: 2px solid #023c24;
  color: black;
  text-align: center;

  p {
    margin: 0;
    font-size: 1.3rem;
  }

  .close {
    background: none;
    border: none;
    font-size: 1.5rem;
    font-weight: bold;
    cursor: pointer;
    position: absolute;
    top: 10px;
    right: 10px;
  }
}
</style>
