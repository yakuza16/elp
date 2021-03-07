<template>
  <CreateTrain msg="Stwórz pociąg" />
</template>

<script>
import CreateTrain from "./components/CreateTrain.vue";

export default {
  name: "App",
  components: {
    CreateTrain,
  },
};
</script>

<style>
body {
  background-color: #2c3e50;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
  margin-top: 60px;
}
</style>
