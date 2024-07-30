<template>
  <div class="code-section">
    <div class="codeTopArea">
      <h3 >{{ title }}</h3>
      <button class="copy-button" @click="copyCode">Ready to use after copying</button>
    </div>
    <div class="code-container" :style="containerStyle">
      <div class="code-scroll-container">
        <pre><code class="language-html" ref="codeBlock"></code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, watch } from 'vue';
import hljs from 'highlight.js/lib/core';
import 'highlight.js/styles/devibeans.css';
import xml from 'highlight.js/lib/languages/xml';
import javascript from 'highlight.js/lib/languages/javascript';
import ClipboardJS from 'clipboard';

const props = defineProps({
  code: {
    type: String,
    required: true
  },
  title: {
    type: String,
    default: ""
  },
  width: {
    type: String,
    default: 'auto'
  },
  height: {
    type: String,
    default: 'auto'
  },
  btnName:{
    type: String,
  }
});

const codeBlock = ref(null);

const initCodeData = () => {
  if (codeBlock.value) {
    codeBlock.value.textContent = props.code;
    hljs.highlightElement(codeBlock.value);
  }
};


hljs.registerLanguage('xml', xml);
hljs.registerLanguage('javascript', javascript);

const containerStyle = computed(() => ({
  width: props.width,
  height: props.height !== 'auto' ? props.height : 'auto',
  overflow: props.height !== 'auto' ? 'hidden' : 'visible'
}));

onMounted(() => {
  initCodeData();
});

const copyCode = () => {
  new ClipboardJS('.copy-button', {
    text: () => props.code
  });

  alert('Code copied to clipboard!');
};
</script>

<style lang="scss" scoped>
.code-section {
  margin-top: 2rem;
  margin-bottom: 2rem;

  .codeTopArea {
    display: flex;
    justify-content: space-between;
    margin-bottom: 0.5rem;
    margin-right: 1rem;

    h3 {
      color: #4a90e2;
    }

    .copy-button {
      background-color: #4a90e2;
      color: white;
      border: none;
      padding: .4rem .8rem;
      border-radius: 5px;
      cursor: pointer;
    }

    .copy-button:hover {
      background-color: #3a7bc8;
    }
  }

  .code-container {
    position: relative;
    border-radius: 10px;
    font-size: 1.2rem;


    .code-scroll-container {
      height: 100%;
      overflow-y: auto;

      &::-webkit-scrollbar {
        width: 8px;
      }

      &::-webkit-scrollbar-track {
        background: #f1f1f1;
        border-radius: 4px;
      }

      &::-webkit-scrollbar-thumb {
        background: #888;
        border-radius: 4px;
      }

      &::-webkit-scrollbar-thumb:hover {
        background: #555;
      }

      pre {
        margin: 0;

        code {
          border-radius: 8px;
          padding: 20px;
          box-shadow:
            inset 1px 1px 3px rgba(255, 255, 255, 0.1),
            inset -1px -1px 3px rgba(0, 0, 0, 0.3);
          display: block;
        }
      }
    }
  }
}
</style>
