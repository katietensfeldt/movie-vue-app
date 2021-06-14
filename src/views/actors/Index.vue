<template>
  <div class="actors-index">
    <h2>Actors</h2>
    Search for an Actor
    <input type="text" v-model="searchTerm" />
    <div v-for="actor in filterBy(actors, searchTerm, 'full_name')" v-bind:key="actor.id">
      <router-link :to="`/actors/${actor.id}`">
        <h4>{{ actor.first_name }} {{ actor.last_name }}</h4>
      </router-link>

      <p>Gender: {{ actor.gender }} | Age: {{ actor.age }}</p>
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
