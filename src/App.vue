<template>
  <div id="app">
    <main-view></main-view>
  </div>
</template>

<script>
import MainView from "@/views/Main.vue";
export default {
  name: "App",
  components: {
    "main-view": MainView,
  },
};
</script>
