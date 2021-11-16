<template>
  <select
    class="form-select"
    name="genres"
    id="genres"
    v-model="selectedGenre"
    @change="$emit('select-genre', selectedGenre)"
  >
    <option selected value="">Select the genre</option>
    <option v-for="(genre, i) in genres" :key="i" :value="genre">
      {{ genre }}
    </option>
  </select>
  <!-- /.form-select -->
</template>

<script>
export default {
  props: {
    genres: [],
  },
  data() {
    return {
      selectedGenre: "",
    };
  },
};
</script>

<style>
</style>