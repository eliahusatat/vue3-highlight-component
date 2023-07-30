<template>
  <pre>
    <code v-html="highlightedCode" class="hljs"></code>
  </pre>
</template>

<script>
import hljs from 'highlight.js';

export default {
  name: 'HighLight',
  props: {
    code: {
      type: String,
      required: true,
    },
    language: {
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
  },
};
</script>

<style src="highlight.js/styles/panda-syntax-dark.css"></style>

