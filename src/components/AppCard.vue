<template>
  <div id="album-card" class="container text-center">
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
  background-color: $header-bg-color;
  width: 200px;
  cursor: pointer;
  transition: transform 0.5s;
  &:hover {
    filter: invert(0.1);
    transform: scale(1.1);
  }
  div {
    padding: 20px 0;
    h6 {
      text-transform: uppercase;
      color: white;
    }
    img {
      box-shadow: 0 0 6px 3px rgba(#000, 0.15);
      width: 100%;
    }
    p {
      margin-bottom: 0;
      color: $text-color;
    }
  }
}
</style>