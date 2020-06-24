<template>
    <div class="edit-box">
      <!--
        对于原生标签，v-model并不等于value+input，内部会对输入法做处理，而且不同的标签解析出的结果不一样 type checkbox = checked + change

        v-model="code"
      :value="code" @input="handleInput"-->
      <textarea :value="code" @input="handleInput" ref="mycode"></textarea>
    </div>
</template>

<script>
//code模版
import codeTemplate from "./lib/codeTemplate";

import "./lib/plugins";

export default {
  data() {
    return {
      code: codeTemplate
    };
  },
  methods: {
    handleInput(e) {
      this.code = e.target.value;

      this.$emit("input", this.code);
    },
    clear() {
      this.code = "";
      this.$emit("input", this.code);
    }
  },
  mounted() {

  }
};
</script>

<style>
.edit-box {
  width:50%;
  height: 100%;
}
.edit-box textarea {
  border: none;
  outline: none;
  height: 100%;
  width: 100%;
}

@import url("./edit.css");
</style>
