<template>
  <div class="cards mt-5">
    <select class="form-select" aria-label="select">
      <option selected>Select the genre</option>
      <option value="jazz">Jazz</option>
      <option value="metal">Metal</option>
      <option value="pop">Pop</option>
      <option value="rock">Rock</option>
    </select>
    <!-- /.form-select -->

    <div
      class="cards_row d-flex justify-content-center flex-wrap"
      v-if="!loading && error === ''"
    >
      <div class="col-lg-2" v-for="album in albums" :key="album.title">
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

    <div class="loading" v-else-if="loading && error === ''">
      <h2 class="text-center text-uppercase">Loading ...</h2>
    </div>
    <!-- /.loading -->

    <div class="error" v-else-if="error != ' '">{{ error }}</div>
    <!-- /.error -->
  </div>
  <!-- ./cards -->
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      albums: [],
      loading: true,
      error: "",
      API_URL: "https://flynn.boolean.careers/exercises/api/array/music",
    };
  },
  mounted() {
    setTimeout(this.callApi, 0);
  },
  methods: {
    callApi() {
      axios
        .get(this.API_URL)
        .then((r) => {
          this.albums = r.data.response;
          this.loading = false;
        })
        .catch((e) => {
          console.log(e);
          this.error = "OPS!";
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