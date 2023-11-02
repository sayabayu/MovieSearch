<template>
  <div>
    <div class="container mt-5">
      <h1 class="title">BY <span class="yo">MOVIE</span></h1>
      <form class="d-flex">
        <input
          class="form-control me-2"
          v-model="searchQuery"
          type="text"
          placeholder="Cari film..."
          aria-label="Search"
        />
        <button
          @click="searchMovies"
          class="btn btn-outline-success"
          type="button"
        >
          Cari
        </button>
      </form>

      <div class="row mt-4">
        <div class="col-md-4" v-for="movie in movies" :key="movie.imdbID">
          <div class="card mb-4">
            <img :src="movie.Poster" class="card-img-top" alt="Poster Film" />
            <div class="card-body">
              <h5 class="card-title">{{ movie.Title }}</h5>
              <p class="card-text"><strong>Tahun:</strong> {{ movie.Year }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: "",
      movies: [],
    };
  },
  methods: {
    async searchMovies() {
      try {
        const apiKey = "90a9b57a";
        const response = await fetch(
          `http://www.omdbapi.com/?s=${this.searchQuery}&apikey=${apiKey}`
        );
        const data = await response.json();
        this.movies = data.Search;
        this.searchQuery = "";
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },
  },
};
</script>

<style scoped>
.title {
  color: #22d988;
  font-weight: 900;
}
.yo {
  color: #043249 !important;
}
</style>
