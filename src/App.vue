<template>
  <div id="app">
    <app-header @customChange="logChange" />
    <main>
      <app-grid />
    </main>
  </div>
</template>

<script>
import AppGrid from "./components/AppGrid.vue";
import AppHeader from "./components/AppHeader.vue";

export default {
  name: "App",
  components: {
    AppHeader,
    AppGrid,
  },
  methods: {
    logChange(event) {
      for (let i = 0; i < event.length; i++) {
        console.log(event[i]);
      }
    },
  },
};
</script>

<style lang="scss">
@import "./assets/styles/general.scss";
</style>
