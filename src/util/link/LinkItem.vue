<template>
  <div class="link-item">
    <div class="linkBtn" @click="changePath(link)">{{ name }}</div>
  </div>
</template>

<script setup>
import { useNavigationStore } from '@/stores/Navigation'

const navigationStore = useNavigationStore();

const props = defineProps({
  link: {
    type: String,
    required: true
  },
  name: {
    type: String,
    required: true
  }
});

const changePath = (newPath) => {
  // 경로 변경
  navigationStore.currentPath = newPath;
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

</script>

<style scoped>
.link-item {
  border-bottom: 1px solid #ffffff;
  padding: 1rem 0;
  color:beige;
}

.linkBtn {
  text-decoration: none;
  color: inherit;
  font-size: inherit;
  font-weight: inherit;
}

.linkBtn:hover {
  color: #d9d997;
  cursor: pointer;
}
</style>