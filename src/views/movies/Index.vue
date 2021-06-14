<template>
  <div class="movies-index">
    <h2>Movies</h2>
    Search by title:
    <input type="text" v-model="titleFilter" />
    <div class="movie" v-for="movie in filterBy(movies, titleFilter, 'title')" v-bind:key="movie.id">
      <router-link :to="`/movies/${movie.id}`">
        <h4>{{ movie.title }} ({{ movie.year }})</h4>
      </router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: () => ({
    movies: [],
    titleFilter: "",
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
