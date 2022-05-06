<template>
  <section
    id="main-grid"
    class="container d-flex justify-content-center align-items-center"
  >
    <div class="row d-flex justify-content-center my-5">
      <div
        v-for="album in albums"
        :key="album.id"
        class="
          d-flex
          justify-content-center
          col-6 col-sm-4 col-md-3 col-lg-2
          m-3
        "
      >
        <app-card :item="album" />
      </div>
    </div>
    <!-- <app-footer v-if="!loading" :len="characterList.length" /> -->
  </section>
</template>

<script>
// import AppLoader from "./AppLoader.vue";
import axios from "axios";
import AppCard from "./AppCard.vue";
export default {
  name: "AppGrid",
  components: {
    // AppLoader,
    AppCard,
  },
  data() {
    return {
      albums: [],
      apiPath: "https://flynn.boolean.careers/exercises/api/array/",
      loading: false,
    };
  },
  mounted() {
    this.loading = true;
    axios
      .get(this.apiPath + "music")
      .then((res) => {
        // console.log(res);
        this.albums = res.data.response;
        console.log(this.albums);
        this.loading = false;
      })
      .catch((error) => {
        console.log(error);
        this.loading = false;
      });
  },
  props: {},
};
</script>

<style scoped lang="scss">
</style>
