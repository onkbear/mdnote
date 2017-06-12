<template>
  <div class="container-full" id="app">
    <navbar></navbar>
    <editor></editor>
  </div>
</template>

<script>
import Editor from './components/Editor'
import Navbar from './components/Navbar'
require('github-markdown-css/github-markdown.css')

export default {
  name: 'app',
  components: {
    Editor,
    Navbar
  }
}
</script>
