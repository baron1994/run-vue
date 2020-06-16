<template>
  <div class="edit">
    <div class="edit-list">
      <button @click="$emit('run')">运行</button>
      <button @click="clear">清空</button>
      {{code}}
    </div>
    <div class="edit-box">
      <!--
        对于原生标签，v-model并不等于value+input，内部会对输入法做处理，而且不同的标签解析出的结果不一样 type checkbox = checked + change

        v-model="code"
      :value="code" @input="handleInput"-->
      <textarea :value="code" @input="handleInput"></textarea>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      code: ""
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
  }
};
</script>

<style>
.edit-list {
  padding: 10px;
  background: #ccc;
}
.edit-list button {
  padding: 10px;
  height: 40px;
  margin: 5px;
}

.edit-box {
  position: absolute;
  top: 60px;
  bottom: 0;
  left: 0;
  right: 0;
}
.edit-box textarea {
  border: none;
  outline: none;
  height: 100%;
  width: 50%;
}
</style>
