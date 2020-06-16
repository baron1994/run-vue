<template>
  <div @click="handleClick">hello world</div>
</template>

<script>
export default {
  methods: {
    handleClick() {
      console.log("click");
    }
  },
  created(){
    console.log('created')
  }
};
</script>

<style>
</style>
