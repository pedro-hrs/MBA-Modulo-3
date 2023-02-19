<template>
  <div>
    <HeaderComponent />
    <CambioComponent />
  </div>
</template>

<script>
import CambioComponent from "@/components/CambioComponent.vue";
import HeaderComponent from "@/components/HeaderComponent.vue";
export default {
  name: "App",
  components: {
    CambioComponent,
    HeaderComponent,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  margin: 0;
  padding: 0;
}
</style>
