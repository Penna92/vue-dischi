<template>
  <div>
    <select
      class="form-select mt-3"
      name="genre"
      id="genre"
      v-model="inputText"
      @change="search"
    >
      <option value="">Musical Genre</option>
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
      inputText: "",
    };
  },
  props: ["musicalGenres"],
  methods: {
    search() {
      this.$emit("search", this.inputText);
      //   this.inputText = "";
    },
    reset() {
      this.inputText = "";
      this.$emit("search", this.inputText);
    },
  },
};
</script>

<style>
</style>