<template>
  <div>
    <select
      class="form-select mt-3"
      name="artist"
      id="artist"
      v-model="selectValue"
      @change="searchArtist"
    >
      <option value="">Musical Artist</option>
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
      selectValue: "",
    };
  },
  props: ["musicalArtists"],
  methods: {
    searchArtist() {
      this.$emit("searchArtist", this.selectValue);
      //   this.selectValue = "";
    },
    // reset() {
    //   this.selectValue = "";
    //   this.$emit("searchArtist", this.selectValue);
    // },
  },
};
</script>

<style>
</style>