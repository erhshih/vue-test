<template>
  <div id="app">
    <TestPage msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import TestPage from "./components/TestPage.vue";

export default {
  name: "App",
  components: {
    TestPage,
  },
};
</script>

<style>
#app {
}
</style>
