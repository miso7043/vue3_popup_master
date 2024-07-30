<template>
  <div class="sourcefrom">
    <h1 v-if="headTitle">{{ headTitle }}</h1>
    source from :
    <a :href="sourcelink"> {{ title || sourcelink }} </a>
  </div>
</template>

<script setup>
import { ref } from 'vue';
const props = defineProps({
  headTitle: {
    type: String,
  },
  sourcelink: {
    type: String,
    required: true
  },
  title: {
    type: String,
    // default: ''
  }
});
</script>

<style scoped>
.sourcefrom {
  font-size: 2rem;
  text-align: center;
  padding-top: 3rem;
  margin-bottom: 2rem;
  color: white;
}
</style>