<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>Add New Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" required class="form-control" v-model="newMovieParams.title" />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" required class="form-control" v-model="newMovieParams.year" />
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <textarea class="form-control" v-model="newMovieParams.plot" />
        <br />
        <small v-if="newMovieParams.plot.length <= 255">{{ 255 - newMovieParams.plot.length }} characters left</small>
        <small v-else-if="newMovieParams.plot.length > 255" class="text-red">
          Too many characters! Movie will not save. Please remove {{ newMovieParams.plot.length - 255 }} characters.
        </small>
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input type="text" class="form-control" v-model="newMovieParams.director" />
      </div>
      <div class="form-group">
        <label>English:</label>
        <input type="checkbox" class="form-control checkbox" checked />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<style scoped>
.text-red {
  color: red;
}
</style>

<script>
import axios from "axios";

export default {
  data: () => ({
    newMovieParams: { plot: "" },
    errors: [],
  }),
  methods: {
    createMovie: function () {
      this.newMovieParams.english = this.checked();
      axios
        .post("/movies", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
    checked: function () {
      return document.querySelector(".checkbox").checked;
    },
  },
};
</script>
