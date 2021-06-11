<template>
  <div class="movies-index">
    <h2>Movies</h2>
    <div class="movie" v-for="movie in movies" v-bind:key="movie.id">
      <router-link :to="`/movies/${movie.id}`">
        <h4>{{ movie.title }} ({{ movie.year }})</h4>
      </router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    movies: [],
  }),
  created: function () {
    axios.get("/movies").then((response) => {
      this.movies = response.data;
      console.log(response.data);
    });
  },
  methods: {},
};
</script>
