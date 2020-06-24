<template>
  <div class="header">
    <div class="title">在线运行Vue组件</div>
    <div class="operation">
      <Button type="text" @click="$emit('run')">
        <Icon type="ios-play-outline" class="btn-icon" />
        <span>运行</span>
      </Button>
      <Button type="text" @click="handleReset()">
        <Icon type="ios-refresh" class="btn-icon" />
        <span>重置</span>
      </Button>
    </div>
    <div class="help">
      <Tooltip placement="bottom-end">
        <div slot="content">
          <p>仿run.iviewui.com</p>
          <p>可在线运行vue组件</p>
          <p>支持iView组件</p>
          <p>支持element-ui组件</p>
        </div>
        <Button type="text">
          <Icon type="ios-help-circle-outline" class="btn-icon" />
        </Button>
      </Tooltip>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    handleReset() {
      this.$Modal.confirm({
        title: "重置确认",
        content: "<p>确认要重置您的代码吗？</p>",
        onOk: () => {
          this.$emit("reset");
          this.$Message.info("代码已重置");
        }
      });
    }
  }
};
</script>

<style scoped>
.header {
  height: 50px;
  line-height: 50px;
  width: 100%;
  padding: 0 40px;
  box-shadow: 0 1px 3px rgba(26, 26, 26, 0.1);
  margin-bottom: 1px;
  box-sizing: border-box;
  background: #fff;

  display: flex;
  flex-direction: row;
}

.title {
  padding-left: 8px;
  font-size: 18px;
  font-weight: bold;
}
.operation {
  display: flex;
  align-items: center;
  font-size: 16px;
  margin-left: 16px;
}

.btn-icon {
  font-size: 20px;
  color: #1296db;
}
</style>