<template>
  <div v-if="isOpen" :class="['slide-in', {'fade-in': isFadeIn}]">
    <div :class="['content', appearDirection]">
      <p>Slide-in Popup</p>
      <SlideBtn @click="handleClose" btnTitle="Close" btnType="btn-rect" fontSize="1.2rem" borderRadius="1rem"
        width="7rem" height="4rem" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import SlideBtn from '../util/SlideButton.vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  appearDirection: {
    type: String,
    default: "up"  // "down", "left", "right"
  }
});

const emit = defineEmits(['close']);

const isFadeIn= ref(false);

const handleClose = () => {
  isFadeIn.value = false;
  setTimeout(() => {
    emit('close');
  }, 300);  // time for transition
};

onMounted(() => {
  if (props.isOpen) {
    isFadeIn.value = true;
  }
});

onUnmounted(() => {
  isFadeIn.value = false;
});
</script>

<style lang="scss" scoped>
.slide-in {
  position: fixed;
  z-index: 1000;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgba(0, 0, 0, 0);
  transition: background-color 0.3s ease;

  &.fade-in {
    background-color: rgba(0, 0, 0, 0.6);
  }

  .content {
    background-color: #2c2c2c;
    padding: 30px;
    border-radius: 1rem;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
    border: 2px solid #023c24;
    color: white;
    text-align: center;
    position: relative;
    max-width: 80%;
    width: 400px;
    display: grid;
    justify-items: center;

    p {
      margin-bottom: 20px;
      font-size: 1.5rem;
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

    &.up {
      animation: slideInUp 0.5s ease-out;
    }

    &.down {
      animation: slideInDown 0.5s ease-out;
    }

    &.left {
      animation: slideInLeft 0.5s ease-out;
    }

    &.right {
      animation: slideInRight 0.5s ease-out;
    }

    @keyframes slideInUp {
      from {
        transform: translateY(300%);
      }

      to {
        transform: translateY(0);
      }
    }

    @keyframes slideInDown {
      from {
        transform: translateY(-300%);
      }

      to {
        transform: translateY(0);
      }
    }

    @keyframes slideInLeft {
      from {
        transform: translateX(-300%);
      }

      to {
        transform: translateX(0);
      }
    }

    @keyframes slideInRight {
      from {
        transform: translateX(300%);
      }

      to {
        transform: translateX(0);
      }
    }
  }
}
</style>
