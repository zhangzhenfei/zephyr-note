<script>
import marked, { Renderer } from 'marked'
import debounce from 'lodash/debounce'
import throttle from 'lodash/throttle'
import highlightjs from 'highlight.js'
import 'highlight.js/styles/default.css'
import 'highlight.js/styles/solarized-light.css'

// Create your custom renderer.
const renderer = new Renderer()
renderer.code = (code, language) => {
  // Check whether the given language is valid for highlight.js.
  const validLang = !!(language && highlightjs.getLanguage(language))
  // Highlight only if the language is valid.
  const highlighted = validLang ? highlightjs.highlight(language, code).value : code
  // Render the highlighted code with `hljs` class.
  return `<pre><code class="hljs solarized-light ${language}">${highlighted}</code></pre>`
}

export default {
  props: {
    isFullWidth: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return { input: '' }
  },
  computed: {
    compiledMarkdown: function () {
      const markOpts = {
        renderer,
        sanitize: true
      }
      return marked(this.input, markOpts)
    }
  },
  methods: {
    update: debounce(function (e) {
      this.input = e.target.value
    }, 300),
    textareaScroll: throttle(function (e) {
      const target = e.target
      const scrollTop = target.scrollTop
      this.$refs.preview.scrollTop = scrollTop
    }, 20)
  }
}
</script>

<template>
  <div class="wrap" :class="{ fullWidth: isFullWidth }">
    <div class="editor">
      <textarea :value="input" @input="update" @scroll="textareaScroll" autofocus></textarea>
    </div>
    <div ref="preview" class="preview clearfix" v-html="compiledMarkdown"></div>
  </div>
</template>


<style lang="scss" scoped>
.wrap {
  position: absolute;
  top: 64px;
  left: 256px;
  right: 0;
  bottom: 0;
  &.fullWidth {
    left: 0;
  }
  .editor,
  .preview {
    float: left;
    width: 50%;
    height: 100%;
    padding: 1em;
  }
  .editor {
    border-right: 1px solid #ccc;
    textarea {
      width: 100%;
      height: 100%;
      overflow-y: scroll;
      border: none;
      resize: none;
      outline: none;
      font-size: 14px;
      font-family: 'Monaco', courier, monospace;
    }
  }
  .preview {
    overflow-y: scroll;
    transition: all .5s;
  }
}
</style>
