<template>
  <div id="md-editor">
    <textarea id="edit-field" v-model="text"></textarea>
    <div id="preview-field">
      <article class="markdown-body" v-html="$options.filters.convertMdToHtml(text)"></article>
    </div>
  </div>
</template>

<script>
import marked from 'marked'
import hljs from 'highlightjs'
import('github-markdown-css/github-markdown.css')
import('highlightjs/styles/github.css')

marked.setOptions({
  renderer: new marked.Renderer(),
  gfm: true,
  tables: true,
  breaks: false,
  pedantic: false,
  sanitize: false,
  smartLists: true,
  smartypants: false,
  xhtml: false,
  highlight: (code, lang) => {
    return hljs.highlightAuto(code, [lang]).value
  }
})

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      text: ''
    }
  },
  filters: {
    convertMdToHtml: function (text) {
      return text ? marked(text) : ''
    },
    highlightMD: function (text) {
      return hljs.highlightAuto(text, ['markdown'])
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
pre {
  background-color: #FF00FF;
}

#md-editor {
  display: flex;
  flex: auto;
  justify-content: center;
  align-self: stretch;
}

#edit-field {
  background-color: #FFF000;
  margin: 0 10px;
  min-width: 500px;
}

#preview-field {
  margin: 0 10px;
  text-align: left !important;
}

</style>
