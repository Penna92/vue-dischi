<template>
  <header class="d-flex justify-content-between align-items-center">
    <img src="../assets/logo.png" alt="Logo" />
    <input
      class="mx-5 h-50"
      type="text"
      placeholder="Filtra album"
      @change="customChange"
    />
  </header>
</template>

<script>
export default {
  methods: {
    customChange(event) {
      this.$emit("customChange", event.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/styles/general.scss";
header {
  height: 80px;
  line-height: 80px;
  width: 100%;
  background-color: $header-bg-color;
  img {
    margin-left: 30px;
    height: 60%;
  }
}
</style>