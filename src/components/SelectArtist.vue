<template>
  <div class="select_artist mb-5">
    <p>Filter by artist:</p>
    <select
      class="form-select m-auto"
      name="artist"
      id="artist"
      v-model="selectedArtist"
      @change="$emit('select-artist', selectedArtist)"
    >
      <option selected value="">All</option>
      <option v-for="(artist, i) in artists" :key="i" :value="artist">
        {{ artist }}
      </option>
    </select>
  </div>
  <!-- /.select_artist -->
</template>

<script>
export default {
  props: {
    artists: [],
  },
  data() {
    return {
      selectedArtist: "",
    };
  },
};
</script>

<style lang="scss">
.select_artist {
  p {
    color: white;
    font-size: 1.1rem;
    font-weight: bold;
    text-align: center;
    text-transform: uppercase;
  }
}
</style>