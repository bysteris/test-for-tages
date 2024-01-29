<template>
  <div id="app">
    <IndexPage />
  </div>
</template>

<script>
import IndexPage from "@/pages/IndexPage";

export default {
  name: "App",
  components: {
    IndexPage,
  },
};
</script>

<style>
#app {
  color: black;
  margin-top: 32px;
}
</style>
