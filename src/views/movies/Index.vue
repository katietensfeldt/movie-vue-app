<template>
  <div class="movies-index">
    <h2>Movies</h2>

    Search by title:
    <input type="text" v-model="titleFilter" />

    <div class="movie" v-for="movie in filterBy(movies, titleFilter, 'title')" v-bind:key="movie.id">
      <div class="row">
        <div class="col-lg-6">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">{{ movie.title }}</h5>
              <p class="card-text">Released {{ movie.year }}</p>
              <router-link :to="`/movies/${movie.id}`" class="btn btn-primary">More info</router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
    <nav aria-label="...">
      <ul class="pagination pagination-lg">
        <li class="page-item">
          <a class="page-link" href="#" aria-label="Previous">
            <span aria-hidden="true">&laquo;</span>
          </a>
        </li>
        <li class="page-item active" aria-current="page">
          <span class="page-link">1</span>
        </li>
        <li class="page-item disabled"><a class="page-link" href="#">2</a></li>
        <li class="page-item disabled"><a class="page-link" href="#">3</a></li>
        <li class="page-item disabled">
          <a class="page-link" href="#" aria-label="Next">
            <span aria-hidden="true">&raquo;</span>
          </a>
        </li>
      </ul>
    </nav>
    <button
      type="button"
      class="btn btn-secondary"
      data-bs-container="body"
      data-bs-toggle="popover"
      data-bs-placement="right"
      data-bs-content="Right popover"
    >
      Popover on right
    </button>
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
