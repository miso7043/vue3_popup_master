<template>
  <div v-if="isOpen" class="tool-tip" :style="tooltipStyle">
    <span class="tooltiptext">{{ txtTooltip }}</span>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  txtTooltip: {
    type: String,
    default: "This is a tooltip"
  }
});

const mouseX = ref(0);
const mouseY = ref(0);

const updateMousePosition = (event) => {
  mouseX.value = event.clientX;
  mouseY.value = event.clientY;
};

onMounted(() => {
  window.addEventListener('mousemove', updateMousePosition);
});

const tooltipStyle = computed(() => ({
  left: `${mouseX.value}px`,
  top: `${mouseY.value - 10}px`, // Subtract 10px so that it is slightly above the cursor
}));
</script>

<style lang="scss" scoped>
.tool-tip {
  position: fixed; // Use 'fixed' instead of 'absolute' to position relative to the viewport
  z-index: 10;
  pointer-events: none; // Allow tooltips to not interfere with mouse events

  .tooltiptext {
    background-color: beige;
    color: #2c2c2c;
    text-align: center;
    border-radius: 1rem;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
    border: 2px solid #023c24;
    font-size: 1.2rem;
    white-space: nowrap;
    position: absolute;
    width: max-content;
    height: auto;
    padding: 1rem 3rem;
    transform: translateY(-100%); // Move the tooltip above the cursor
  }
}
</style>
