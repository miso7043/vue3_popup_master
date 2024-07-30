<template>
  <div class="menuPageBottom">
    <div class="prevNext">
      <img src="@/assets/icon/iconr-prev.svg" v-if="prevBtnActive" @click="clickPrevNext('slideInLeft', $event)"
        class="prevBtn btnActive" alt="" />
      <img src="@/assets/icon/iconr-prev.svg" v-if="!prevBtnActive" class="prevBtn dimmedBtn" alt="" />

      <div class="curItem">{{ selectedItemName }}</div>
      <img src="@/assets/icon/iconr-next.svg" v-if="nextBtnActive" @click="clickPrevNext('slideInRight', $event)"
        class="nextBtn btnActive" alt="" />
      <img src="@/assets/icon/iconr-next.svg" v-if="!nextBtnActive" class="nextBtn dimmedBtn" alt="" />
    </div>


    <div class="linkContainer" v-for="mainItem in reorderedMenuList" :key="mainItem.id">
      <LinkItem :link="mainItem.link" :name="mainItem.name" class="sub-main" />
      <LinkItem v-for="(menu, index) in mainItem.submenu" :key="index" :link="menu.link" :name="menu.name"
        class="sub-item" />
      <hr />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useMenuInfoStore } from '@/stores/menuInfo';
import { useNavigationStore } from '@/stores/Navigation'
import { useRouter } from 'vue-router';
import LinkItem from './LinkItem.vue';
import 'animate.css';

const props = defineProps({
  id_step_1: {
    type: String,
    required: true
  },
  id_step_2: {
    type: String,
    required: true
  },
  linkLast: {
    type: String,
    required: true
  }
});

const navigationStore = useNavigationStore();
const menuInfoStore = useMenuInfoStore();
const menuInfo = ref(menuInfoStore.menuInfo);
const reorderedMenuList = ref(null);
const selectedItemName = ref(null);
const prevBtnActive = ref(true);
const nextBtnActive = ref(true);
let _curSubMenuItems = [];

const router = useRouter();

const clickPrevNext = (animation, $e) => {
  const aniElement = $e.target;
  aniElement.className = aniElement.classList[0];

  animateCSS(aniElement, animation);

  let selectedIndex = getSelectedIndex(_curSubMenuItems, props.linkLast);
  if (animation == "slideInLeft") {
    selectedIndex -= 1;
  } else {
    selectedIndex += 1;
  }

  // 경로 변경
  navigationStore.currentPath = _curSubMenuItems[selectedIndex].link;
  window.location.href = _curSubMenuItems[selectedIndex].link;

  console.log(_curSubMenuItems[selectedIndex].link);

  resetPrevNextBtn(selectedIndex);
}

const animateCSS = (element, aniType) => {
  const prefix = 'animate__';

  // We create a Promise and return it
  new Promise((resolve, reject) => {
    const animationName = `${prefix}${aniType}`;
    element.classList.add(`${prefix}animated`, animationName);

    // 애니메이션이 종료 되었을 때, 받는 이벤트이다.
    function handleAnimationEnd(event) {
      event.stopPropagation();
      element.classList.remove(`${prefix}animated`, animationName);

      // 이 다음에서 then으로 이어서 받을 수 있다.
      // 여기선 필요없음.
      resolve('Animation ended');
    }

    // { once: true } 한번 호출된 후에는 자동으로 이벤트리스너를 제거한다.
    element.addEventListener('animationend', handleAnimationEnd, { once: true });
  });
}

const getSelectedIndex = (arr, lastLinkPart) => {
  // function getSelectedIndex(arr, lastLinkPart) {
  const index = arr.findIndex(item => {
    const linkParts = item.link.split('/');
    return linkParts[linkParts.length - 1] === lastLinkPart;
  });

  return index;
}

onMounted(() => {
  // Find the menu item with id_step_1
  const mainItem = menuInfo.value.find(item => item.id === props.id_step_1);

  _curSubMenuItems = getSubMenuItems(mainItem);
  const selectedIndex = getSelectedIndex(_curSubMenuItems, props.linkLast);

  // if(props.id_step_2 == "admin"){
  if (selectedIndex < 0) {
    prevBtnActive.value = false;
    nextBtnActive.value = false;
    return;
  }


  if (selectedIndex > -1) {
    selectedItemName.value = _curSubMenuItems[selectedIndex].name;
    reorderedMenuList.value = mainItem.submenu;
  } else {
    const subItem = mainItem.submenu.find(item => item.id === props.linkLast);
    selectedItemName.value = subItem.name
  }

  resetPrevNextBtn(selectedIndex);
});

const resetPrevNextBtn = (selectedIndex) => {

  if (selectedIndex > 0) {
    prevBtnActive.value = true;
  } else {
    prevBtnActive.value = false;
  }

  if (selectedIndex < _curSubMenuItems.length - 1) {
    nextBtnActive.value = true;
  } else {
    nextBtnActive.value = false;
  }
};

const getSubMenuItems = (mainItem) => {
  // function getSubMenuItems(mainItem) {
  let menuItems = [];

  if (mainItem) {
    // Find the index of the subMenu item with id_step_2
    const subMenuIndex = mainItem.submenu.findIndex(subItem => subItem.id === props.id_step_2);

    if (subMenuIndex > 0) {
      // 첫번째 항목이 아닐 경우는 배열 순서를 바꾸어준다.

      // Move the found subMenu item to the first position
      const [subMenuItem] = mainItem.submenu.splice(subMenuIndex, 1);
      mainItem.submenu.unshift(subMenuItem);
    }

    menuItems = mainItem.submenu[0].submenu;
  }

  return menuItems;
}
</script>

<style scoped>
* {
  width: 100%;
}

.menuPageBottom {
  width: 100%;
  margin-inline: auto;
  background-color: #323232;
}

.prevNext {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
  padding-top: 2rem;
}

.prevBtn,
.nextBtn {
  cursor: pointer;
  width: 3rem;
  height: auto;
}

.prevBtn {
  margin-left: 5rem;
}

.nextBtn {
  margin-right: 5rem;
}

.curItem {
  text-align: center;
  font-size: 1.5rem;
  color:#d1dbe3;
}

.btnActive {
  cursor: pointer;
}

.dimmedBtn {
  opacity: 0.3;
  cursor: default;
}

.linkContainer{
  margin: 0 2rem;
  padding-left: 3rem;
  padding-right: 7rem;
}

.sub-main {
  font-size: 1.2rem;
  font-weight: 700;
}

.sub-item {
  margin-left: 2rem;
  font-size: 1rem;
  font-weight: 500;
  width: calc(100% - 2rem);
}

hr {
  margin: 1rem 0;
}
</style>