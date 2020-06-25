<template>
  <div id="app">
    <Header @run="run" @reset="reset" />
    <div class="main">
      <Split v-model="split">
        <!-- 左边代码区域 -->
        <codemirror slot="left" ref="mycodemirror" v-model="code" :options="cmOptions" />
        <!-- 右边运行区域 -->
        <Show slot="right" :code="code" ref="show" />
      </Split>
    </div>
  </div>
</template>

<script>
import Header from "@/components/header";
//code模版
import codeTemplate from "@/components/edit/lib/codeTemplate.js";
//vue-codemirror相关
import { codemirror } from "vue-codemirror";
import "@/components/edit/lib/plugins";
import "@/components/edit/edit.css";
import Show from "@/components/show";

export default {
  name: "App",
  data() {
    return {
      code: codeTemplate,
      split: 0.5,
      cmOptions: {
        mode: "text/x-vue",
        tabSize: 2,
        lineNumbers: true, //行号
        scrollbarStyle: "simple",
        autoCloseBrackets: true, //自动补全括号
        showCursorWhenSelecting: true, //select显示光标
        autoCloseTags: true,
        matchTags: { bothTags: true },
        foldGutter: true, //可折叠的块
        minFoldSize: 3, // 有bug 改了库文件 'codemirror/addon/fold/foldcode.js' 里面的defaultOptions
        gutters: [
          "CodeMirror-linenumbers",
          "CodeMirror-foldgutter",
          "CodeMirror-lint-markers"
        ],
        styleActiveLine: true
      }
    };
  },
  components: {
    Header,
    codemirror,
    Show
  },
  methods: {
    run() {
      // console.log("run");
      this.$refs.show.reset();
      this.$refs.show.run();
    },
    reset() {
      // console.log("reset");
      this.$refs.show.reset();
      this.code = codeTemplate;
      this.$nextTick(() => {
        // this.$refs.show.run();
      });
    }
  },
  mounted() {
    //解决嵌套使用codemirror时，点击才会显示的问题。
    var timer = setTimeout(() => {
      this.$refs.mycodemirror.codemirror.refresh();
      clearTimeout(timer);
    }, 0);
  }
};
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
}

.main {
  position: absolute;
  z-index: -1;
  top: 50px;
  left: 0;
  right: 0;
  bottom: 0;
}
</style>
