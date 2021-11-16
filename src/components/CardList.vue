<template>
  <div class="cards mt-5">
    <div class="filter">
      <SelectGenre :genres="genresList" @select-genre="filterGenre" />
      <!-- /.select_genre -->

      <SelectArtist :artists="artistsList" @select-artist="filterArtist" />
      <!-- /.select_artist -->
    </div>
    <!-- /.filter -->

    <div
      class="cards_row d-flex justify-content-center flex-wrap"
      v-if="!loading"
    >
      <div class="col-lg-2" v-for="(album, i) in getFilteredAlbums" :key="i">
        <div class="card text-center my-2 rounded-0">
          <img :src="album.poster" :alt="album.title" class="img-fluid" />
          <h4 class="text-uppercase mt-3 mb-4">{{ album.title }}</h4>
          <p class="py-0 my-0">{{ album.author }}</p>
          <p class="py-0 my-0">{{ album.year }}</p>
        </div>
        <!-- /.card -->
      </div>
    </div>
    <!-- /.cards -->

    <div class="loading" v-else-if="loading">
      <h2 class="text-center text-uppercase">Loading ...</h2>
    </div>
    <!-- /.loading -->
  </div>
  <!-- ./cards -->
</template>

<script>
import SelectGenre from "./SelectGenre.vue";
import SelectArtist from "./SelectArtist.vue";
import axios from "axios";

export default {
  components: {
    SelectGenre,
    SelectArtist,
  },
  data() {
    return {
      albums: [],
      loading: true,
      API_URL: "https://flynn.boolean.careers/exercises/api/array/music",
      selectedGenre: "",
      genresList: [],
      selectedArtist: "",
      artistsList: [],
    };
  },
  mounted() {
    setTimeout(this.callApi, 500);
  },
  methods: {
    callApi() {
      axios
        .get(this.API_URL)
        .then((r) => {
          this.albums = r.data.response;

          this.albums.forEach((album) => {
            //popolo array genresList
            if (!this.genresList.includes(album.genre)) {
              this.genresList.push(album.genre);
            }

            //popolo array artistsList
            if (!this.artistsList.includes(album.author)) {
              this.artistsList.push(album.author);
            }
          });

          this.loading = false;
        })
        .catch((e) => {
          console.log(e);
        });
    },
    filterGenre(event) {
      this.selectedGenre = event;
    },
    filterArtist(event) {
      this.selectedArtist = event;
    },
  },
  computed: {
    getFilteredAlbums() {
      return this.albums.filter((album) => {
        return album.genre.includes(this.selectedGenre);
      });
    },
  },
};
</script>

<style lang="scss">
@import "../assets/scss/variables.scss";

.cards {
  .card {
    width: calc(150px + 3rem);
    height: 350px;
    margin: auto;
    padding: 1.5rem;
    background-color: $light_background_color;

    img {
      max-width: 150px;
      margin: auto;
    }

    h4 {
      color: white;
      font-size: 1.2rem;
      font-weight: bold;
    }

    p {
      color: $text_gray_color;
      font-size: 1.1rem;
    }
  }
  .loading {
    color: white;
    font-weight: bold;
  }
}
</style>