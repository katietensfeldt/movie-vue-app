<template>
  <div class="movies-edit">
    <form v-on:submit.prevent="updateMovie()">
      <h1>Edit Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="editMovieParams.title" />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="editMovieParams.year" />
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <textarea class="form-control" v-model="editMovieParams.plot" />
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input type="text" class="form-control" v-model="editMovieParams.director" />
      </div>
      <div class="form-group">
        <label>English:</label>
        <input
          type="checkbox"
          class="form-control checkbox"
          v-model="editMovieParams.english"
          v-on:click="isChecked()"
        />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    editMovieParams: {},
    errors: [],
  }),
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      this.editMovieParams = response.data;
      console.log(response.data);
    });
  },
  methods: {
    updateMovie: function () {
      axios
        .patch(`/movies/${this.editMovieParams.id}`, this.editMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/movies/${response.data.id}`);
        })
        .catch((error) => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
    isChecked: function () {
      this.editMovieParams.english = document.querySelector(".checkbox").checked;
    },
  },
};
</script>
