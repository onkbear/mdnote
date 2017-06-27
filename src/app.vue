<template>
  <div class="container-full" id="app">
    <navbar v-on:download='download'></navbar>
    <editor v-on:applyInput='applyInput' ref="editor"></editor>
  </div>
</template>

<script>
import Editor from './components/Editor'
import Navbar from './components/Navbar'
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
      let blob = new Blob([this.input], {'type': 'text/plain'})
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
    }
  }
}
</script>
