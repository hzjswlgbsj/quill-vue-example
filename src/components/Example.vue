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
// import { quillEditor } from "vue-quill-editor";
import { quillEditor } from "quill-vue";
import "quill-vue/dist/static/css/quill-vue.css";

export default {
  components: {
    quillEditor
  },

  data() {
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
            [{ indent: "-1" }, { indent: "+1" }],
            [{ direction: "rtl" }],
            [{ size: ["small", false, "large", "huge"] }],
            [{ header: [1, 2, 3, 4, 5, 6, false] }],
            [{ font: [] }],
            [{ color: [] }, { background: [] }],
            [{ align: [] }],
            ["link", "image", "video", "formula"],
            ["clean"]
          ],
          syntax: {
            highlight: text => hljs.highlightAuto(text).value
          }
        }
      }
    };
  },

  methods: {
    onEditorBlur(editor) {
      console.log("editor blur!", editor);
    },
    onEditorFocus(editor) {
      console.log("editor focus!", editor);
    },
    onEditorChange(editor) {
      console.log("editor change!", editor);
    },
    onEditorReady(editor) {
      this.quill = editor;
      console.log("editor ready!", editor);
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
