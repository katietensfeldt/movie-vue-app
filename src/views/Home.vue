<template>
  <div class="home">
    <h2>Movies</h2>
    <h3>Create a new movie</h3>
    <input type="text" v-model="newTitle" placeholder="Title" />
    <br />
    <input type="text" v-model="newYear" placeholder="Year" />
    <br />
    <input type="text" v-model="newPlot" placeholder="Plot" />
    <br />
    <input type="text" v-model="newDirector" placeholder="Director" />
    <br />
    <input type="text" v-model="newEnglish" placeholder="English? true or false" />
    <br />
    <button v-on:click="addMovie">Add movie</button>
    <div class="movies">
      <h3>Movie List</h3>
      <div class="movie" v-for="movie in movies" v-bind:key="movie.id">
        <h4>{{ movie.title }} ({{ movie.year }})</h4>
        <button v-on:click="showInfo(movie)">More Info</button>
      </div>
      <dialog id="movie-details">
        <form method="dialog">
          <h1>Movie Info</h1>
          <p>Title: {{ currentMovie.title }}</p>
          <p>Year: {{ currentMovie.year }}</p>
          <p>Director: {{ currentMovie.director }}</p>
          <p>Plot: {{ currentMovie.plot }}</p>
          <button>Close</button>
        </form>
      </dialog>
    </div>
  </div>
</template>

<style scoped>
.movies {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.movie {
  border: 1px solid black;
  margin: 10px;
  padding: 5px;
  width: 50%;
}
</style>

<script>
import axios from "axios";

export default {
  data: () => ({
    movies: [],
    newTitle: "",
    newYear: "",
    newPlot: "",
    newDirector: "",
    newEnglish: "",
    currentMovie: {},
  }),
  created: function () {
    this.allMovies();
  },
  methods: {
    allMovies: function () {
      axios.get("/movies").then((response) => {
        this.movies = response.data;
        console.log(response.data);
      });
    },
    addMovie: function () {
      let params = {
        title: this.newTitle,
        year: this.newYear,
        plot: this.newPlot,
        director: this.newDirector,
        english: this.newEnglish,
      };
      axios
        .post("/movies", params)
        .then((response) => {
          this.movies.push(response.data);
          console.log(response.data);
          this.newTitle = "";
          this.newYear = "";
          this.newPlot = "";
          this.newDirector = "";
          this.newEnglish = "";
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
    showInfo: function (movie) {
      this.currentMovie = movie;
      console.log(movie);
      document.querySelector("#movie-details").showModal();
    },
  },
};
</script>
