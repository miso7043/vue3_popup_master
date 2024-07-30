<template>
  <div class="pageContainer">
    <section class="pageContainer-list">
      <h3>{{ "Types of Popups" }}</h3>
      <div v-for="(popup, index) in popComponentList" :key="index" class="popup-type">
        <h4>{{ popInfoList[`txt_${2 * (index + 1) - 1}`] }}</h4>
        <p>{{ popInfoList[`txt_${2 * (index + 1)}`] }}</p>

        <div class="btnGroup">
          <ToggleBtn class="openPop" @click="fnOpenPop(index)" @mouseenter="fnHoverPop(index)"
            @mouseleave="fnLeavePop(index)" btnType="btn-outline" btnTitle="open popup" fontSize="1.2rem"
            borderRadius="1.8rem" height="3.5rem" color="orange" backgroundColor="#ffffff11"/>

        </div>

        <!-- code box component -->
        <component :is="codeComponentList[index]" />
      </div>
    </section>

    <!-- Popup Component -->
    <component :is="popComponentList[activePopupIndex]" v-if="isPopupActive" :isOpen="isPopupActive"
      @close="fnClosePop" />
  </div>
</template>

<script setup>
import { shallowRef, ref, computed, onMounted } from 'vue';
import { defineAsyncComponent } from 'vue';
import ToggleBtn from '../util/ToggleButton.vue';

import PopModal from './Modal.vue';
import PopConfirm from './Confirm.vue';
import PopLogin from './Login.vue';
import PopNotification from './Notification.vue';
import PopImage from './ImagePop.vue';
import PopPromotion from './Promotion.vue';
import PopTooltip from './Tooltip.vue';
import PopToast from './Toast.vue';
import PopSlideIn from './SlideIn.vue';
import PopFullScreen from './FullScreenPop.vue';

import CodeModal from './CodeModal.vue';
import CodeConfirm from './CodeConfirm.vue';
import CodeLogin from './CodeLogin.vue';
import CodeNotification from './CodeNotification.vue';
import CodeImage from './CodeImagePop.vue';
import CodePromotion from './CodePromotion.vue';
import CodeTooltip from './CodeTooltip.vue';
import CodeToast from './CodeToast.vue';
import CodeSlideIn from './CodeSlideIn.vue';
import CodeFullScreen from './CodeFullScreenPop.vue';


const popInfoList = {
    txt_1: "1. Basic Modal Popup",
    txt_2: "Basic modal popups block user interaction and prevent other actions until the user closes the popup",
    txt_3: "2. Confirmation Dialog",
    txt_4: "A popup that asks users to confirm or cancel an action. For example, requesting user confirmation before deleting data",
    txt_5: "3. Login Form Modal",
    txt_6: "A popup that provides a form for user authentication. Users enter and submit login information",
    txt_7: "4. Notification Popup",
    txt_8: "A popup that provides important information or alerts to users. Generally used to attract user attention.",
    txt_9: "5. Image Preview Popup",
    txt_10: "Used to preview large images or videos",
    txt_11: "6. Promotion Popup",
    txt_12: "A popup that displays special offers or advertisements",
    txt_13: "7. Tooltip Popup",
    txt_14: "A popup that appears when hovering over a specific element to provide additional information or explain usage",
    txt_15: "8. Toast Popup",
    txt_16: "A popup that appears and disappears briefly on the screen to display status messages such as success, error, or information",
    txt_17: "9. Slide-in Popup",
    txt_18: "A popup that slides in from a specific direction on the screen",
    txt_19: "10. Fullscreen Popup",
    txt_20: "A popup that covers the entire screen to prevent users from interacting with elements outside the popup and provide important information that requires focus.",
}

const ToastMsg = "A new message has arrived!"


const popComponentList = shallowRef([
  PopModal, PopConfirm, PopLogin,
  PopNotification, PopImage, PopPromotion,
  PopTooltip, PopToast,
  PopSlideIn, PopFullScreen
]);

const codeComponentList = shallowRef([
  CodeModal, CodeConfirm, CodeLogin,
  CodeNotification, CodeImage, CodePromotion,
  CodeTooltip, CodeToast,
  CodeSlideIn, CodeFullScreen
]);

const isPopupActive = ref(false);
const activePopupIndex = ref(-1);
const tooltipIndex = computed(() => popComponentList.value.findIndex(comp => comp === PopTooltip));

const fnOpenPop = (index) => {
  if (index !== tooltipIndex.value) {
    activePopupIndex.value = index;
    isPopupActive.value = true;
  }
}

const fnClosePop = () => {
  isPopupActive.value = false;
  activePopupIndex.value = -1;
}

const fnHoverPop = (index) => {
  if (index === tooltipIndex.value) {
    activePopupIndex.value = index;
    isPopupActive.value = true;
  }
}

const fnLeavePop = (index) => {
  if (index === tooltipIndex.value) {
    isPopupActive.value = false;
    activePopupIndex.value = -1;
  }
}

/* <svg :data="svgContent" v-html="svgContent"></svg> */
const svgContent = ref('');

onMounted(async () => {
  const response = await fetch('/src/assets/icon/icon-github.svg');
  const svgText = await response.text();
  svgContent.value = svgText;
});

const gitAddress = 'https://github.com/';
const openGitSite = () => {
  window.open(gitAddress, '_blank', 'noopener,noreferrer');
}


</script>

<style lang="scss" scoped>
.pageContainer {
  width: 100%;
  margin: 0 !important;
  text-align: left;

  h3 {
    border-bottom: 2px solid #3498db;
    padding-bottom: 10px;
    margin-bottom: 1rem;
  }

  .pageContainer-list {
    .popup-type {
      border-radius: 5px;
      padding: 1rem;
      margin-bottom: 1rem;
      border-bottom: 1px solid #3498db33;

      .btnGroup {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(min-content, max-content));
        grid-auto-flow: column;
        justify-content: start;
        align-items: center;
        gap: 2rem;

        margin-top: 1rem;

        .svg-container {
          // display: inline-block;
          cursor: pointer;
          border: 2px solid #008CBA;
          border-radius: 2rem;
          padding: 0.6rem 1.2rem;
          background-color: #ffffff11;
          transition: background-color 0.3s ease;

          svg{
            width: 108px;
            height: 30px;
          }
          &:hover {
            background-color: orange;

            :deep(.subClass) {
              fill: white;
            }
          }

          :deep(.subClass) {
            fill: black;
            transition: fill 0.3s ease;
          }
        }
      }
    }
  }
}
</style>