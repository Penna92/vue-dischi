<template>
  <div>
    <select
      class="form-select mt-3"
      name="genre"
      id="genre"
      v-model="selectValue"
      @change="searchGenre"
    >
      <option value="">Genre</option>
      <option :value="genre" v-for="genre in musicalGenres" :key="genre">
        {{ genre }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "AppSelectGenre",
  data() {
    return {
      selectValue: "",
    };
  },
  props: ["musicalGenres"],
  methods: {
    searchGenre() {
      this.$emit("searchGenre", this.selectValue);
      //   this.selectValue = "";
    },
    // reset() {
    //   this.selectValue = "";
    //   this.$emit("search", this.selectValue);
    // },
  },
};
</script>

<style>
</style>