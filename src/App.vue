<template>
  <div id="app">
    <navbar></navbar>
    <editor></editor>
  </div>
</template>

<script>
import Editor from './components/Editor'
import Navbar from './components/Navbar'

export default {
  name: 'app',
  components: {
    Editor,
    Navbar
  }
}
</script>
