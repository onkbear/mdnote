<template>
  <nav class="navbar navbar-inverse navbar-fixed-top">
    <div class="container-fluid">
      <div class="navbar-header">
        <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
          <span class="sr-only">Toggle navigation</span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
        </button>
        <a class="navbar-brand" href="#">mdnote</a>
      </div>
      <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
        <ul class="nav navbar-nav navbar-right">
          <li class="dropdown">
            <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Download <span class="caret"></span></a>
            <ul class="dropdown-menu">
              <li><a href="#" v-on:click="downloadMarkdown">Markdown</a></li>
              <li><a href="#" v-on:click="downloadHTML">HTML</a></li>
            </ul>
          </li>
        </ul>
      </div><!-- /.navbar-collapse -->
    </div>
  </nav>
</template>

<script>
export default {
  name: 'navbar',
  methods: {
    downloadMarkdown: function () {
      this.$emit('download', 'md')
    },
    downloadHTML: function () {
      this.$emit('download', 'html')
    }
  }
}
</script>
