<template>
  <div class="select_genre mb-5">
    <p>Filter by genre:</p>
    <select
      class="w-25 form-select m-auto"
      name="genres"
      id="genres"
      v-model="selectedGenre"
      @change="$emit('select-genre', selectedGenre)"
    >
      <option selected value="">All</option>
      <option v-for="(genre, i) in genres" :key="i" :value="genre">
        {{ genre }}
      </option>
    </select>
  </div>
  <!-- /.select_genre -->
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

<style lang="scss">
.select_genre {
  p {
    color: white;
    font-size: 1.1rem;
    font-weight: bold;
    text-align: center;
    text-transform: uppercase;
  }
}
</style>