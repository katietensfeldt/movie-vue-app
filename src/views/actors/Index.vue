<template>
  <div class="actors-index">
    <h2>Actors</h2>
    <div v-for="actor in actors" v-bind:key="actor.id">
      <router-link :to="`/actors/${actor.id}`">
        <h4>{{ actor.first_name }} {{ actor.last_name }}</h4>
      </router-link>

      <p>Gender: {{ actor.gender }} | Age: {{ actor.age }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    actors: [],
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
