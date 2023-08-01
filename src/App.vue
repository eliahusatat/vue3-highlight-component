<template>
  <HighLight :with-header="true" language="js" header-language="JavaScript" :code="code"/>
</template>

<script>
// import HighLight from "vue3-highlight-component";
import HighLight from "./components/HighLight"

export default {
  name: 'App',
  components: {
    HighLight
  },
  data() {
    return {
      code: `function factorialRecursive(n) {
  if (n === 0 || n === 1) {
    return 1;
  } else {
    return n * factorialRecursive(n - 1);
  }
}

const number = 5;
const result = factorialRecursive(number);`
    }
  },
}
</script>

<style src="highlight.js/styles/panda-syntax-dark.css"></style>
