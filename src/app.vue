<template>
  <div class="container-full" id="app">
    <navbar v-on:download='download'></navbar>
    <editor v-on:applyInput='applyInput' ref="editor"></editor>
  </div>
</template>

<script>
import Editor from './components/editor'
import Navbar from './components/navbar'
import marked from 'marked'
window.jQuery = window.$ = require('jquery')
require('github-markdown-css/github-markdown.css')
require('bootstrap-sass/assets/javascripts/bootstrap.min.js')

export default {
  name: 'app',
  data () {
    return {
      input: '',
      fileName: 'untitled'
    }
  },
  components: {
    Editor,
    Navbar
  },
  methods: {
    applyInput: function (input) {
      this.input = input
    },
    download: function (extension) {
      this.$refs.editor.$emit('apply-event')
      let fileName = this.fileName + '.' + extension
      let blob = this.generateBlob(extension)

      let url = (window.URL || window.webkitURL)
      let downloadUrl = url.createObjectURL(blob)

      // Create link element
      let element = document.createElement('a')
      element.href = downloadUrl
      element.download = fileName
      element.style.display = 'none'
      document.body.appendChild(element)
      element.click()
      document.body.removeChild(element)
      url.revokeObjectURL(downloadUrl)
    },
    generateBlob: function (extension) {
      if (extension === 'md') {
        return new Blob([this.input], {'type': 'text/plain'})
      } else if (extension === 'html') {
        // Compile
        let compiledHtml = marked(this.input, { sanitize: true })
        // Append missing tags
        compiledHtml = '<!DOCTYPE html><html><head><meta charset="utf-8"></head><body>' + compiledHtml + '</body></html>'
        return new Blob([compiledHtml], {'type': 'text/html'})
      }
    }
  }
}
</script>
