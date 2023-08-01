<template>
  <div :class="{'code-block' : withHeader}">
    <div v-if="withHeader" class="code-header">
      <div class="lang text-header">{{currentLang}}</div>
      <div @click="copyToClipboard" class="copy-btn flex gap-2">
        <svg  v-if="codeCopyText === copyText" stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24"  class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg">
          <path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path>
          <rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect>
        </svg>
        <svg v-else class="h-5 w-4" width="1em" height="1em" xmlns="http://www.w3.org/2000/svg">
          <line x1="0.1em" y1="0.5em" x2="0.4em" y2="0.8em" stroke="currentColor" stroke-width="0.1em" />
          <line x1="0.4em" y1="0.8em" x2="0.9em" y2="0.2em" stroke="currentColor" stroke-width="0.1em" />
        </svg>
        <span class="text-header"> {{ codeCopyText }}</span>
      </div>
    </div>
    <pre :class="{code : withHeader}">
      <code v-html="highlightedCode" class="hljs code-box"></code>
    </pre>
  </div>
</template>

<script>
import hljs from 'highlight.js';

export default {
  name: 'HighLight',
  data() {
    return {
      codeCopyText : this.copyText,
    };
  },
  methods: {
    // eslint-disable-next-line no-unused-vars
    copyToClipboard(el) {
      if (navigator.clipboard) {
        navigator.clipboard.writeText(this.code).then(
            () => {this.setSuccessTransitions()
            },
            () => {}
        )
      }
    },
    setSuccessTransitions() {
      clearTimeout(this.successTimeout)
      this.codeCopyText = this.copySuccessText;
      this.successTimeout = setTimeout(() => {
        this.codeCopyText = this.copyText;
      }, 1000)
    }
  },
  props: {
    code: {
      type: String,
      required: true,
    },
    language: {
      type: String,
      default: '',
    },
    withHeader: {
      type: Boolean,
      default: false,
    },
    copyText: {
      type: String,
      default: 'Copy code',
    },
    copySuccessText: {
      type: String,
      default: 'Copied!',
    },
    headerLanguage: {
      type: String,
      default: '',
    },
  },
  computed: {
    highlightedCode() {
      const language = this.language || hljs.highlightAuto(this.code).language;
      const { value } = hljs.highlight(this.code,{language});
      return value;
    },
    currentLang() {
      return this.headerLanguage || this.language || hljs.highlightAuto(this.code).language;
    },
  },
};
</script>
<style scoped src="../assets/css/style.css"></style>



