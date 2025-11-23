<template>
  <div class="codeBox">
    <CodeViewer :code="codeData" :title="codeFileName" height="400px" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import CodeViewer from '../util/CodeViewer.vue';

const codeFileName = "Login.vue";
const codeData = `<template>
  <div v-if="isOpen" class="modal">
    <div class="modal-content">
      <h2>Login</h2>
      <input type="text" placeholder="Username" v-model="username" />
      <input type="password" placeholder="Password" v-model="password" />
      <div class="btnBox">
        <SlideBtn @click="fn_login" btnTitle="Login" btnType="btn-rect" fontSize="1.2rem" borderRadius="1rem"
          width="7rem" height="4rem" />
        <SlideBtn @click="fn_cancel" btnTitle="Cancel" btnType="btn-rect" fontSize="1.2rem" borderRadius="1rem"
          width="7rem" height="4rem" />
      </div>
    </div>
  </div>
</template>

<\script setup>
import { ref } from 'vue';
import SlideBtn from '../util/SlideButton.vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    required: true
  }
})

const username = ref('')
const password = ref('')

const fn_login = () => {
  // Implement login logic
  

  fn_cancel()
}

const emit = defineEmits(['close'])

const fn_cancel = () => {
  emit('close')
}
</\script>

<style lang="scss" scoped>
.modal {
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


  .modal-content {
    background-color: #2c2c2c;
    margin: auto;
    padding: 30px;
    border-radius: 1rem;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
    max-width: 80%;
    width: 400px;
    text-align: center;
    border: 2px solid #023c24;
    color: white;
    display: grid;
    justify-items: center;

    .btnBox {
      margin-top: 1rem;
      display: grid;
      justify-items: center;
      grid-template-columns: repeat(2, 1fr);
      gap: 1rem;
    }

    h2 {
      margin-top: 0;
      font-size: 2rem;
      color: white;
    }

    input {
      width: calc(100% - 40px); // Width considering padding
      margin: 10px 0;
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      font-size: 1rem;
      outline: none;

      &::placeholder {
        color: #ccc;
      }
    }
  }
}
</style>
`;
</script>

<style lang="scss" scoped>
</style>