<template>
  <div class="editor">
    <div class="row">
      <div class="col-xs-6">
        <div class="codemirror">
          <codemirror :options="editorOption"
                      @change="update">
          </codemirror>
        </div>
      </div>
      <div class="col-xs-6">
        <div class="markdown-body" v-html="compiledMarkdown"></div>
      </div>
    </div>
  </div>
</template>

<script>
import marked from 'marked'
import 'lodash'
export default {
  name: 'editor',
  data () {
    return {
      input: '',
      editorOption: {
        value: '',
        tabSize: 2,
        styleActiveLine: true,
        lineNumbers: true,
        line: true,
        foldGutter: true,
        styleSelectedText: true,
        mode: 'markdown',
        theme: 'monokai'
      }
    }
  },
  created: function () {
    this.$on('apply-event', this.applyInput)
  },
  computed: {
    compiledMarkdown: function () {
      return marked(this.input, { sanitize: true })
    }
  },
  methods: {
    update: _.debounce(function (value) {
      this.input = value
    }, 300),
    applyInput: function () {
      this.$emit('applyInput', this.input)
    }
  }
}
</script>
