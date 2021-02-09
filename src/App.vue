<template>
  <AddWagon msg="Stwórz pociąg" />
</template>

<script>
import AddWagon from "./components/AddWagon.vue";

export default {
  name: "App",
  components: {
    AddWagon,
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
