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
    <AppSelectGenre
      @searchGenre="setSearchGenre($event)"
      :musicalGenres="genres"
    />
    <AppSelectArtist
      @searchArtist="setSearchArtist($event)"
      :musicalArtists="artists"
    />
    <app-loader v-if="loading" />
    <div class="row d-flex justify-content-around my-5">
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
import AppSelectArtist from "./AppSelectArtist.vue";
export default {
  name: "AppGrid",
  components: {
    AppLoader,
    AppCard,
    AppSelectGenre,
    AppSelectArtist,
  },
  data() {
    return {
      albums: [],
      apiPath: "https://flynn.boolean.careers/exercises/api/array/",
      loading: false,
      genres: [],
      artists: [],
      searchText: "",
    };
  },
  methods: {
    setSearchGenre(text) {
      // this.searchText = "";
      this.searchText = text;
      // console.log(text);
      // reset();
    },
    setSearchArtist(text2) {
      // this.searchText = "";
      this.searchText = text2;
      console.log(text2);
      console.log(this.text);
      // reset();
    },
  },
  computed: {
    filteredList() {
      if (this.searchText === "") {
        return this.albums;
      }
      return this.albums.filter((el) => {
        return el.genre === this.searchText || el.author === this.searchText;
      });
    },
    // filteredListArtist() {
    //   if (this.searchText === "") {
    //     return this.albums;
    //   }
    //   return this.albums.filter((el) => {
    //     return el.author === this.searchText;
    //   });
    // },
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
            if (!this.artists.includes(el.author)) {
              this.artists.push(el.author);
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
