<template>
  <div id="app">
    <Header />
    <div class="app-content">
      <AppContent />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import AppContent from "./components/AppContent.vue";

export default {
  name: "App",
  components: {
    Header,
    AppContent
  }
};
</script>

<style>
body {
  margin: 0;
}

#app {
  margin: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.app-content {
  display: flex;
  align-content: stretch;
}
</style>
