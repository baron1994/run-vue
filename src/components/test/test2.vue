<template>
  <div>
    <com1 v-bind:parentmsg="msg"></com1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: "啊-父组件中的数据"
    };
  },
  components: {
    com1: {
      data() {
        return {
          title: "123",
          content: "qqq"
        };
      },
      template: '<h1 @click="change">这是子组件---{{ parentmsg }}</h1>',
      props: ["parentmsg"],
      methods: {
        change() {
          this.parentmsg = "被修改了";
        }
      }
    }
  }
};
</script>

<style>
</style>