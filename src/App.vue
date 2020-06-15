<template>
  <div id="app">
    <Edit />
    <Show />
  </div>
</template>

<script>
import Edit from "@/components/edit.vue";
import Show from "@/components/show.vue";

export default {
  name: "App",
  components: {
    Edit,
    Show
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
html,
body,
#app {
  width: 100%;
  height: 100%;
}
#app {
  display: flex;
}
#app > div {
  width: 50%;
  height: 100%;
}
</style>
