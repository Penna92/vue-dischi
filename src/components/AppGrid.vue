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
    <h3 class="my-5 text-danger" v-if="filteredList.length === 0 && !loading">
      Nessun album corrisponde ai criteri da te selezionati
    </h3>
    <div
      v-if="filteredList.length > 0"
      class="row d-flex justify-content-around my-5"
    >
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
      searchText2: "",
      // chosenGenre: false,
    };
  },
  methods: {
    setSearchGenre(text) {
      // this.chosenGenre = true;
      this.searchText = text;
    },
    setSearchArtist(text2) {
      this.searchText2 = text2;
    },
  },
  computed: {
    filteredList() {
      if (this.searchText === "" && this.searchText2 === "") {
        return this.albums;
      }
      return this.albums.filter((el) => {
        if (this.searchText === "" && this.searchText2 !== "") {
          return el.genre === this.searchText || el.author === this.searchText2;
        } else if (this.searchText !== "" && this.searchText2 === "") {
          return el.genre === this.searchText || el.author === this.searchText2;
        } else {
          return el.genre === this.searchText && el.author === this.searchText2;
        }
      });
    },
  },
  mounted() {
    this.loading = true;
    setTimeout(() => {
      axios
        .get(this.apiPath + "music")
        .then((res) => {
          // console.log(res);
          this.albums = res.data.response;
          this.albums.forEach((el) => {
            if (!this.genres.includes(el.genre)) {
              this.genres.push(el.genre);
            }
            if (!this.artists.includes(el.author)) {
              this.artists.push(el.author);
            }
          });
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
