<template>
  <div id="album-card" class="container d-flex text-center">
    <div>
      <img class="" :src="item.poster" alt="" />
      <h6 class="my-3">{{ item.title }}</h6>
      <p>{{ item.author }}</p>
      <p>{{ item.year }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppCard",
  props: ["item"],
};
</script>

<style lang="scss" scoped>
@import "../assets/styles/variables.scss";
#album-card {
  width: 200px;
  min-width: 200px;
  background-color: $header-bg-color;
  cursor: pointer;
  transition: transform 0.5s;
  &:hover {
    background-color: lighten($header-bg-color, 10%);
    // filter: invert(0.1);
    transform: scale(1.1);
  }
  div {
    width: 100%;
    padding: 20px 0;
    h6 {
      text-transform: uppercase;
      color: white;
    }
    img {
      box-shadow: 0 0 6px 3px rgba(#000, 0.15);
      width: 100%;
      // height: 100px;
    }
    p {
      margin-bottom: 0;
      color: $text-color;
    }
  }
}
</style>