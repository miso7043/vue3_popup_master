<template>
    <video autoplay loop muted plays-inline class="video-back">
      <source :src="videoSrc" :type="videoType" />
    </video>
  </template>
  
  <script setup>
  
  // props 정의
  const props = defineProps({
    videoSrc: {
      type: String,
      required: true
    },
    videoType: {
      type: String,
      required: true
    }
  });
  </script>
  
  <style scoped>
  .video-back {
    position: absolute;
    margin-inline: auto;
    width:100%;
    height: 100%;
    object-fit: cover; /* 비디오 비율을 유지하면서 영역에 꽉 차게 만듦 */
    z-index: -1;
  }
  </style>
  