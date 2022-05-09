<template>
  <section
    id="main-grid"
    class="
      container
      d-flex
      flex-column
      justify-content-center
      align-items-center
    "
  >
    <AppSelectGenre @search="setSearchGenre($event)" :musicalGenres="genres" />
    <app-loader v-if="loading" />
    <div class="row d-flex justify-content-center my-5">
      <div
        v-for="album in filteredList"
        :key="album.index"
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
import AppLoader from "./AppLoader.vue";
import axios from "axios";
import AppCard from "./AppCard.vue";
import AppSelectGenre from "./AppSelectGenre.vue";
export default {
  name: "AppGrid",
  components: {
    AppLoader,
    AppCard,
    AppSelectGenre,
  },
  data() {
    return {
      albums: [],
      apiPath: "https://flynn.boolean.careers/exercises/api/array/",
      loading: false,
      genres: [],
      searchText: "",
    };
  },
  methods: {
    setSearchGenre(text) {
      this.searchText = text;
    },
  },
  computed: {
    filteredList() {
      if (this.searchText === "") {
        return this.albums;
      }
      return this.albums.filter((el) => {
        return el.genre === this.searchText;
      });
    },
  },
  mounted() {
    this.loading = true;
    setTimeout(() => {
      axios
        .get(this.apiPath + "music")
        .then((res) => {
          console.log(res);
          this.albums = res.data.response;
          this.albums.forEach((el) => {
            if (!this.genres.includes(el.genre)) {
              this.genres.push(el.genre);
            }
          });
          // console.log(this.albums);
          this.loading = false;
        })
        .catch((error) => {
          console.log(error);
          this.loading = false;
        });
    }, 2000);
  },
};
</script>

<style scoped lang="scss">
</style>
