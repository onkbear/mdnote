<template>
  <textarea></textarea>
</template>

<script>
  import CodeMirror from 'codemirror'
  require('codemirror/lib/codemirror.css')
  require('codemirror/mode/meta')
  require('codemirror/mode/markdown/markdown.js')
  require('codemirror/addon/selection/active-line.js')
  require('codemirror/theme/monokai.css')
  export default {
    data: function () {
      return {
        content: ''
      }
    },
    props: {
      options: {
        required: true
      }
    },
    mounted: function () {
      var _this = this
      this.editor = CodeMirror.fromTextArea(this.$el, this.options)
      this.editor.on('change', function (cm) {
        _this.content = cm.getValue()
        _this.$emit('change', _this.content)
      })
      this.editor.setOption('extraKeys', {
        Tab: function (cm) {
          var spaces = Array(cm.getOption('indentUnit') + 1).join(' ')
          cm.replaceSelection(spaces)
        }
      })
    }
  }
</script>
