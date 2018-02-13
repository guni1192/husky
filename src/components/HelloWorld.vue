<template>
  <div>
    <div id="file-util">
      <input type="file" id="md-file-in" @change="importMDFile">
      <a class="btn" :href="downloadUrl" @click="exportMDFile">export</a>
      {{ downloadUrl }}
    </div>
    <hr />
    <div id="md-editor">
      <textarea id="edit-field" v-model="text"></textarea>
      <div id="preview-field">
        <article class="markdown-body" v-html="$options.filters.convertMdToHtml(text)"></article>
      </div>
    </div>
  </div>
</template>

<script>
import marked from 'marked'
import hljs from 'highlightjs'
import FileSaver from 'filesaver.js'
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
      text: '',
      downloadUrl: ''
    }
  },
  filters: {
    convertMdToHtml: function (text) {
      return text ? marked(text) : ''
    },
    highlightMD: function (text) {
      return hljs.highlightAuto(text, ['markdown'])
    }
  },
  methods: {
    importMDFile: function (event) {
      const file = event.target.files
      const reader = new FileReader()
      reader.readAsText(file[0])
      reader.onload = event => { this.text = reader.result }
    },
    exportMDFile: function (event) {
      const blob = new Blob([this.text], {type: 'text/markdown;charset=utf-8'})
      FileSaver.saveAs(blob, 'hoge.md')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#md-editor {
  display: flex;
  flex: auto;
  justify-content: center;
  align-self: stretch;
}

#edit-field {
  background-color: #FFFFF0;
  margin: 0 10px;
  min-width: 500px;
}

#preview-field {
  margin: 0 10px;
  text-align: left !important;
  min-width: 500px;
}

</style>
