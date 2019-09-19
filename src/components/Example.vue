<template>
  <div class="editor-container">
    <quill-editor
      class="quill-vue-editor"
      ref="myTextEditor"
      v-model="content"
      :options="editorOption"
      height="960px"
      @blur="onEditorBlur($event)"
      @focus="onEditorFocus($event)"
      @change="onEditorChange($event)"
      @ready="onEditorReady($event)"
    >
      <div slot="toolbar"></div>
    </quill-editor>
  </div>
</template>

<script>
import hljs from "highlight.js";
import "highlight.js/styles/androidstudio.css";
import "quill/dist/quill.core.css";
import "quill/dist/quill.snow.css";
import "quill/dist/quill.bubble.css";
import { QuillEditor } from "quill-vue";
import "quill-vue/dist/static/css/quill-vue.css";

export default {
  components: {
    QuillEditor
  },

  data() {
    // const src = 'https://lib.sixtyden.com/%E8%BF%BD%E5%85%89%E8%80%85mv.mp4';
    // const src = 'https://player.youku.com/embed/XMzQ4ODE3NDQ4MA=='; // youku播放地址
    // const src = 'https://www.youtube.com/watch?v=qI9xIe9KtVU'; // youtube播放地址
    hljs.configure({
      languages: ["javascript", "ruby", "python"]
    });
    return {
      quill: {},
      content: "",
      editorOption: {
        modules: {
          toolbar: [
            ["bold", "italic", "underline", "strike"],
            ["blockquote", "code-block"],
            [{ header: 1 }, { header: 2 }],
            [{ list: "ordered" }, { list: "bullet" }],
            [{ script: "sub" }, { script: "super" }],
            [{ size: ["small", false, "large", "huge"] }],
            [{ header: [1, 2, 3, 4, 5, 6, false] }],
            [{ font: [] }],
            [{ color: [] }, { background: [] }],
            [{ align: [] }],
            ["link", "image", "video-another", "iframe", "vuecomp", "formula"],
            ["clean"]
          ],
          syntax: {
            highlight: text => hljs.highlightAuto(text).value
            // hljs: text => hljs.highlightAuto(text).value
          }
        }
      }
    };
  },

  methods: {
    onEditorBlur(editor) {
      // console.log("editor blur!", editor);
    },
    onEditorFocus(editor) {
      // console.log("editor focus!", editor);
    },
    onEditorChange(editor) {
      console.log("editor change!", editor);
    },
    onEditorReady(editor) {
      this.quill = editor;
      // console.log("editor ready!", editor);
    }
  }
};
</script>

<style scoped>
.editor-container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.quill-vue-editor {
  margin-top: 20px;
  width: 816px;
}
</style>
