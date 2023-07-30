# vue3-highlight-component


## Usage

```vue
<template>
  <HighLight language="js" :code="code"/>
</template>

<script>
import hljs from 'highlight.js'
import HighLight from "vue3-highlight-component";

// Register the language if it's not supported by default
hljs.registerLanguage('js', require('highlight.js/lib/languages/javascript'))

export default {
  name: 'App',
  data() {
    return {
      code: `your js code...`
    }
  },
  components: {
    HighLight
  }
}
</script>
<!-- you can choose alot of diffrent styles from highlight.js/styles -->
<style src="highlight.js/styles/panda-syntax-dark.css"></style>
```

Prop `language` is optional since highlight.js could automatically infer the language if it's not set.

