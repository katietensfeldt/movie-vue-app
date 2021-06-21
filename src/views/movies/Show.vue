<template>
  <div class="movies-show">
    <h2>{{ movie.title }}</h2>
    <p>Year: {{ movie.year }}</p>
    <p>Director: {{ movie.director }}</p>
    <p>
      Plot:
      <br />
      {{ movie.plot }}
    </p>
    <p v-if="movie.english">Language: English</p>
    <router-link :to="`/movies/${movie.id}/edit`">Edit</router-link>
    |
    <button v-on:click="destroyMovie()">Delete</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    movie: {},
  }),
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      this.movie = response.data;
      console.log(response.data);
    });
  },
  methods: {
    destroyMovie: function () {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios.delete(`/movies/${this.movie.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        });
        console.log("Destroyed!");
      }
    },
  },
};
</script>
