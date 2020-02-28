<template>
  <div id="app">
    <QRBranded brand-image-src="boomerang-with-text.png" text="happy :-)" :size="300" color-dark="#748793" />
  </div>
</template>

<script>
import QRBranded from "./components/QRBranded";
export default {
  name: "App",
  components: {
    QRBranded
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
