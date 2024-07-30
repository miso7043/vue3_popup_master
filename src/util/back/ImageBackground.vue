<template>
  <img :src="imgSrc" :alt="imgAlt">
  </template>
  
  <script setup>
  
  // props 정의
  const props = defineProps({
    imgSrc: {
      type: String,
      required: true
    },
    imgAlt: {
      type: String
    }
  });
  </script>
  
  <style scoped>
  img {
    position: absolute;
    margin-inline: auto;
    width:100%;
    height: 100%;
    object-fit: cover; /* 이미지 비율을 유지하면서 영역에 꽉 차게 만듦 */
    z-index: -1;
  }
  </style>
  