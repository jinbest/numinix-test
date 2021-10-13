<template>
  <div id="app">
    <Header />
    <home-page />
  </div>
</template>

<script>
import Header from "./components/Header";
import HomePage from "./pages/HomePage";

export default {
  name: "App",
  components: {
    Header,
    HomePage,
  },
};
</script>

<style>
@import "./assets/style/font.css";

body,
p,
h1,
h2,
h3 {
  padding: 0;
  margin: 0;
}
#app {
  font-family: "Rubik";
  text-align: center;
  background: #f2f5fa;
  min-height: 100vh;
}
</style>
