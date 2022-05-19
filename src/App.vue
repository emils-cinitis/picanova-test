<template>
  <div id="app">
    <Header></Header>
    <router-view />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Header from "@/components/Header/Header.vue";

@Component({
  components: {
    Header
  }
})
export default class App extends Vue {
}
</script>

<style lang="scss">
body {
  margin: 0;
  background-color: rgb(97, 97, 97);
  min-height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
