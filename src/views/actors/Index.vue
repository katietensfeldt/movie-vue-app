<template>
  <div class="actors-index">
    <h2>Actors</h2>
    Search for an Actor
    <input type="text" v-model="searchTerm" />
    <div
      v-for="actor in filterBy(actors, searchTerm, 'full_name')"
      v-bind:key="actor.id"
      class="card mb-3"
      style="max-width: 540px"
    >
      <div class="row g-0">
        <div class="col-md-4">
          <img :src="actor.image" class="img-fluid rounded-start" alt="Actor image" />
        </div>
        <div class="col-md-8">
          <div class="card-body">
            <h5 class="card-title">{{ actor.full_name }}</h5>
            <p class="card-text">Age: {{ actor.age }} | Gender: {{ actor.gender }}</p>
            <router-link :to="`/actors/${actor.id}`" type="button" class="btn btn-info">More Info</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: () => ({
    actors: [],
    searchTerm: "",
  }),
  created: function () {
    axios.get("/actors").then((response) => {
      this.actors = response.data;
      console.log(response.data);
    });
  },
  methods: {},
};
</script>
