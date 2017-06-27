<template>
  <div class="container-full" id="app">
    <navbar></navbar>
    <editor></editor>
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
  components: {
    Editor,
    Navbar
  }
}
</script>
