<template>
  <div>
    <select
      class="form-select mt-3"
      name="artist"
      id="artist"
      v-model="selectValue2"
      @change="searchArtist"
    >
      <option value="">Artist</option>
      <option :value="artist" v-for="artist in musicalArtists" :key="artist">
        {{ artist }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "AppSelectArtist",
  data() {
    return {
      selectValue2: "",
    };
  },
  props: ["musicalArtists"],
  methods: {
    searchArtist() {
      this.$emit("searchArtist", this.selectValue2);
      //   this.selectValue2 = "";
    },
    // reset() {
    //   this.selectValue2 = "";
    //   this.$emit("searchArtist", this.selectValue2);
    // },
  },
};
</script>

<style>
</style>